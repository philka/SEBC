## latest available version
```
[root@ip-10-0-60-244 ec2-user]# curl -X GET -u "admin:admin" http://ip-10-0-60-244.us-west-2.compute.internal:7180/api/version
v13
```

## cm version
```
[root@ip-10-0-60-244 ec2-user]# curl -X GET -u "admin:admin" http://ip-10-0-60-244.us-west-2.compute.internal:7180/api/v13/cm/version | grep version
  "version" : "5.8.2",
```

## cm users
```
[root@ip-10-0-60-244 ec2-user]# curl -X GET -u "admin:admin" http://ip-10-0-60-244.us-west-2.compute.internal:7180/api/v13/users
{
  "items" : [ {
    "name" : "admin",
    "roles" : [ "ROLE_ADMIN" ]
  }, {
    "name" : "philka",
    "roles" : [ "ROLE_LIMITED" ]
  } ]

```

## Report the database server in use by CM
```
[root@ip-10-0-60-244 ec2-user]# curl -X GET -u "admin:admin" http://ip-10-0-60-244.us-west-2.compute.internal:7180/api/v13/cm/log 2>&1 | grep -o 'jdbcUrl":"[^"]*' | sort | uniq
jdbcUrl":"jdbc:mysql://localhost/scm?useUnicode=true&characterEncoding=UTF-8
```