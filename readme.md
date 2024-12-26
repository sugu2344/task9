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

 #### 2) Find all the company drives which appeared between 15 oct-2020 and 31-oct-2020

```sql
 db.company_drives.find({
  date: { $gte: "2020-10-15", $lte: "2020-10-31" }
});
``` 
#### 3) Find all the company drives and students who are appeared for the placement.
```sql
db.company_drives.aggregate([
  {
    $lookup: {
      from: "users",
      localField: "users_appeared",
      foreignField: "_id",
      as: "students"
    }
  }
]);
```

<!-- #### 4) Find all the company drives and students who are appeared for the placement. -->