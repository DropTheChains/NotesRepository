对用户表进行crud

```Java
@PostMapping("/save")  
public Result save(@RequestBody User user){  
    int returnid = iuserService.save(user);  
    return Result.success(returnid);  
}  
@GetMapping("/{id}")  
public Result getById(@PathVariable Integer id){  
    return Result.success(iuserService.getById(id));  
}  
  
@PostMapping("/update")  
public Result update(@RequestBody User user){  
    return Result.success(iuserService.update(user));  
}


@Override  
public Integer save(User user) {  
    Date date = new Date();  
    String s = IdUtil.fastSimpleUUID();  
    String format = DateUtil.format(date, "yyyyMMdd");  
    String cradid = format + s;  
    cradid = cradid.substring(0, 16);  
    user.setCardid(cradid);  
    return userMapper.save(user);  
}  
  
@Override  
public User getById(Integer id) {  
    User byId = userMapper.getById(id);  
    return byId;  
}  
  
@Override  
public Integer update(User user) {  
    return userMapper.update(user);  
}


<select id="getById" resultType="com.chains.library.entity.User">  
    select * from user where id = #{id}  
</select>

<insert id="save" useGeneratedKeys="true" keyProperty="id">  
    insert into user(name,username,age,sex,phone,address,cardid)  
    values(#{ name },#{username},#{age},#{sex},#{phone},#{address},#{cardid})  
</insert>  
  
<update id="update">  
    update user set  
    name = #{name},username = #{username},age = #{age},sex = #{sex},phone =#{phone} ,address =#{address}  
    where id = #{id}  
</update>

```

前端页面
```JavaScript
<template>
    <div>
        <h2>新增会员页面</h2>
        
        <el-form v-model="form">
            <el-form-item label="姓名">
                <el-input v-model="form.name" placeholder="请输入姓名："></el-input>
            </el-form-item>
            <el-form-item label="用户名">
                <el-input v-model="form.username" placeholder="请输入用户名："></el-input>
            </el-form-item>
            <el-form-item label="年龄">
                <el-input v-model="form.age" placeholder="请输入年龄："></el-input>
            </el-form-item>
            <el-form-item label="性别">
                <el-input v-model="form.sex" placeholder="请输入性别："></el-input>
            </el-form-item>
            <el-form-item label="联系方式">
                <el-input v-model="form.phone" placeholder="请输入联系方式："></el-input>
            </el-form-item>
            <el-form-item label="地址">
                <el-input v-model="form.address" placeholder="请输入地址："></el-input>
            </el-form-item>
        </el-form>
        <div>
        <el-button @click="save">新增</el-button>
        <el-button @click="reset">重置</el-button>
        </div>
    </div>
</template>

<script>
import request from '@/common/request'

export default ({
    name: "addUser",
    data() {
        return {
            form: {

            }
        }
    },
    methods: {
        save() {
            request.post('/user/save',this.form).then( res =>{
                if( res.code === '200'){
                    this.$notify.success('新增成功')
                }else{
                    this.$notify.error(res.msg)
                }
            })
        },
        reset(){
            this.form = {}
        }
    },  
    
})
</script>

```

```JavaScript
<template>
    <div>
        <h2>修改会员页面</h2>
        
        <el-form v-model="form">
            <el-form-item label="姓名">
                <el-input v-model="form.name" placeholder="请输入姓名："></el-input>
            </el-form-item>
            <el-form-item label="用户名">
                <el-input v-model="form.username" placeholder="请输入用户名："></el-input>
            </el-form-item>
            <el-form-item label="年龄">
                <el-input v-model="form.age" placeholder="请输入年龄："></el-input>
            </el-form-item>
            <el-form-item label="性别">
                <el-input v-model="form.sex" placeholder="请输入性别："></el-input>
            </el-form-item>
            <el-form-item label="联系方式">
                <el-input v-model="form.phone" placeholder="请输入联系方式："></el-input>
            </el-form-item>
            <el-form-item label="地址">
                <el-input v-model="form.address" placeholder="请输入地址："></el-input>
            </el-form-item>
        </el-form>
        <div>
        <el-button @click="editUser">修改</el-button>
        <el-button @click="reset">重置</el-button>
        </div>
    </div>
</template>

<script>
import request from '@/common/request'
export default ({
    name: "editUser",
    data() {
        return {
            form:{

            }
        };
    },
    methods: {
        getById(){
            const id = this.$route.query.id
            request.get('/user/' + id).then( res =>{
                this.form = res.data
            })
        },
        editUser(){
            request.post('/user/update',this.form).then(res => {
                if( res.code === '200'){
                    this.$notify.success('修改成功')
                }else{
                    this.$notify.error(res.msg)
                }
            })
        },
        reset(){
            this.getById()
        }
    },
    created() {
        this.getById()
    },
})
</script>

```
