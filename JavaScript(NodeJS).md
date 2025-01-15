# Migrating from JavaScript(NodeJS)
```javascript
const db = require('../db/users');
//Use for encryption user's password
const bcrypt = require('bcryptjs');
const jwt = require('jsonwebtoken');
const config= require('../config');

exports.reguser = (req, res) => {
    const userinfo = req.body;
    // if (!userinfo.username || !userinfo.password) {
    //     // return res.send({status: 1, message: 'Input username or password!'});
    //     return res.cc('Input username or password!');
    // }
    const sqlStr = 'select * from ev_users where username=?';
    const regStr = 'insert into ev_users (username, password) values (?, ?)';
    const verSrtr = 'select * from ver where username=? and ver=?';

    db.query(verSrtr, [userinfo.username,userinfo.ver], (err, results) => {
        if (err) return res.cc(err);
        if (results.length !== 1) return res.cc('Failed Search userinfo!');
        //Encryption user's password
        userinfo.password = bcrypt.hashSync(userinfo.password, 10);
        // res.send({status: 0, message: 'reguser OK', data: userinfo});
        db.query(regStr, [userinfo.username, userinfo.password], (err, results) => {
            if (err) return res.cc(err);
            if (results.affectedRows === 1) return res.cc('ok', 0);
        });
    })

    db.query(sqlStr, userinfo.username, (err, results) => {
        if (err) return res.cc(err);
        if (results.length > 0) return res.cc('The username already exists!');
    });

};

exports.login = (req, res) => {
    const userinfo = req.body;

    const loginStr = 'select * from ev_users where username=?';
    db.query(loginStr, userinfo.username, (err, results) => {
        if (err) return res.cc('err');
        if (results.length !== 1) return res.cc('Log in Failed!');
        const compareResult = bcrypt.compareSync(userinfo.password, results[0].password);
        if (!compareResult) return res.cc('Wrong Password!');
        //console.log(results);
        const user = {...results[0], password:'',user_pic:''};
        const tokenStr = jwt.sign(user, config.jwtSecretKey, {expiresIn: '10h'});
        return res.send({
            status: 0,
            message:'Successful Login! Jumping...',
            token: 'Bearer ' + tokenStr,
            redirectUrl: `./index.html?token=${encodeURIComponent('Bearer ' + tokenStr)}`
        });
    });
};

exports.delete = (req, res) => {
    const deleteInfo = req.body;
    if (!deleteInfo.username) return res.send({status: 1, message: 'Input username you want to delete!'});
    const sqlStr = 'select * from ev_users where username=?';
    const delStr = 'delete from ev_users where username=?';
    db.query(sqlStr, deleteInfo.username, (err, results) => {
        if (err) return res.send({status: 1, message: err.message});
        if (results.length > 0) {
            return db.query(delStr, deleteInfo.username, (err, results) => {
                if (err) return res.cc(err);
                if (results.affectedRows === 1) return res.cc('ok', 0);
            });
        }else {
            return res.cc('The user does not exists!');
        }
    });

};

exports.test = (req, res) => {
    db.query('select id,username from ev_users', (err, results) => {
        return res.cc('ok', 0,results);
    })
};
```
