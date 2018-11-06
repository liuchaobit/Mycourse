# 测控技术与仪器毕业设计选题系统

#### 2018秋季学期

---

## [毕设选题系统](https://bs.liuchaos.cn/)

---

#### 系统状态：测试阶段

---
## 选题流程

```flow 
st=>start: 开始 
e=>end: 登录 
io1=>inputoutput: 输入用户名密码 
sub1=>subroutine: 数据库查询子类 
cond=>condition: 是否有此用户 
cond2=>condition: 密码是否正确 
op=>operation: 读入用户信息

st->io1->sub1->cond 
cond(yes,right)->cond2 
cond(no)->io1(right) 
cond2(yes,right)->op->e 
cond2(no)->io1 
```

---

