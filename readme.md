# **MongoDB Task**

## Create a database named Zen.

```sql
use zen;
```

- #### collections

```sql
db.createCollection("users");

```

```sql
db.createCollection("codekata");

```

```sql
db.createCollection("attendance");

```

```sql
db.createCollection("topics");

```

```sql
db.createCollection("tasks");

```

```sql
db.createCollection("company_drives");

```

```sql
db.createCollection("mentors");

```

# **Queries**

 #### 1) Find all the topics and tasks which are thought in the month of October

```sql
  db.topics.find({ date: { $regex: "2020-10" } });
``` 
