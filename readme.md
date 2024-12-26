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

#### 4) Find the number of problems solved by the user in codekata

```sql
db.codekata.find({}, { user_id: 1, problems_solved: 1 });
```
#### 5) Find all the mentors with who has the mentee's count more than 15
```sql
db.mentors.find({ mentees_count: { $gt: 15 } });

```

#### 5) Find the number of users who are absent and task is not submitted  between 15 oct-2020 and 31-oct-2020
```sql
db.attendance.aggregate([
  {
    $match: {
      status: "absent",
      date: { $gte: "2020-10-15", $lte: "2020-10-31" }
    }
  },
  {
    $lookup: {
      from: "tasks",
      localField: "user_id",
      foreignField: "submitted_by",
      as: "tasks"
    }
  },
  {
    $match: { "tasks.0": { $exists: false } }
  },
  {
    $group: { _id: null, count: { $sum: 1 } }
  }
]);
```