# **mybatis**

1. #{}和${}的区别是什么？

   - #{}是预处理编译，${}是字符串替换
   - mybatis在处理#{}时，会将sql中的#{}替换为？号，调用PreparedStatement的set方法来赋值
   - mybaits在处理${}时，会将${}替换为变量的值
   - 使用#{}可以有效的防止SQL注入，提高系统的安全性

2. 当实体类中的属性名和表中的字段名不一样时，该怎么办？

   1. 在sql语句中定义字段的别名使其与属性名对应
   2. 通过<resultMap>来映射字段名和实体类属性名使其一一对应

   ```xml
    <select id="getOrder" parameterType="int" resultMap="orderresultmap">
           select * from orders where order_id=#{id}
    </select>
    <resultMap type=”me.gacl.domain.order” id=”orderresultmap”> 
        <!–用id属性来映射主键字段–> 
        <id property=”id” column=”order_id”> 
        <!–用result属性来映射非主键字段，property为实体类属性名，column为数据表中的属性–> 
        <result property = “orderno” column =”order_no”/> 
        <result property=”price” column=”order_price” /> 
    </reslutMap>
   ```

   

3. 模糊查询like语句该怎么写？

   1. ​	在Java代码中添加通配符

   ```xml
    string wildcardname = “%smi%”; 
       list<name> names = mapper.selectlike(wildcardname);
   
       <select id=”selectlike”> 
        select * from foo where bar like #{value} 
       </select>
   ```

   	2.	在sql语句中拼接通配符，会引起sql注入

   ```xml
    string wildcardname = “smi”; 
       list<name> names = mapper.selectlike(wildcardname);
   
       <select id=”selectlike”> 
        select * from foo where bar like "%"#{value}"%"
       </select>
   ```

4. 通常一个xml映射文件，都会有一个Dao接口与之对应，这个Dao接口的工作原理是什么？Dao接口里的方法，参数不同时，方法可以重载吗

   - Dao接口即Mapper接口，Dao接口的全限定类名即xml映射文件的namespace的值，Dao接口中的方法名即xml映射文件中MappedStatement的id值，接口方法内的参数，就是传递给sql的参数。Mapper接口是没有实现类的，当调用接口方法时，接口全限定类名+方法名可以定位到唯一的MappedStatement。
   - Dao接口中的方法是不能重载的，因为是全限定类名+方法名的保存和寻找策略。
   - Dao接口的工作原理是动态代理，mabatis运行时会使用JDK动态代理为Dao接口生成代理proxy对象，代理对象proxy会拦截接口方法，转而执行MappedStatement所代表的sql语句，然后将sql执行结果返回。

5. mybatis如何进行分页，分页插件的原理是什么？

   - mybatis使用RowBounds对象进行分页，它是针对ResultSet结果执行的内存分页，而非物理分页，可以在sql内直接书写带有物理分页的参数来实现物理分页功能（limit）。

   - 分页插件的原理是通过mybatis提供的插件接口，实现自定义插件，在拦截方法内拦截sql，然后重写sql

     