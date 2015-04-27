## db 쿼리 실행

```
$ result = ActiveRecord::Base.connection.execute("SELECT * FROM users")
$ result.each {|mysql_result| puts mysql_result; puts}
```

