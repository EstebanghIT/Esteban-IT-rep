# SQL Support Troubleshooting Lab

## Overview

A basic SQL lab created to practice using database queries to investigate common Technical Support and Application Support scenarios.

The goal was to understand how support teams can use SQL to verify information stored in a database when troubleshooting user or application issues.

## Test Database

I worked with a small test database containing information about:

- Users
- Support tickets
- Ticket status
- Priority
- Created dates

## Basic Queries

### Finding a User

```sql
SELECT *
FROM users
WHERE username = 'testuser';
```

This can be useful when checking whether a user exists in the database or reviewing their stored information.

### Finding Open Tickets

```sql
SELECT *
FROM tickets
WHERE status = 'Open';
```

### Finding High Priority Tickets

```sql
SELECT *
FROM tickets
WHERE priority = 'High';
```

### Sorting Recent Tickets

```sql
SELECT *
FROM tickets
ORDER BY created_date DESC;
```

### Using JOIN

```sql
SELECT users.username,
       tickets.ticket_id,
       tickets.status
FROM users
JOIN tickets
ON users.user_id = tickets.user_id;
```

This makes it possible to see which support tickets belong to each user.

## Support Scenario

A user reports that ticket 1024 appears incorrectly in the application.

I can check the stored information using:

```sql
SELECT ticket_id, status, priority
FROM tickets
WHERE ticket_id = 1024;
```

If the database shows the ticket as resolved but the application still displays it as open, this gives useful information for further troubleshooting. The issue may require investigation of the application, API, caching, or synchronization process rather than the stored database value.

## Troubleshooting Process

1. Identify the affected user or record
2. Query the relevant table
3. Filter the results
4. Compare the stored data with the reported behavior
5. Document the findings
6. Escalate when necessary

## Tools Used

- SQL
- SQLite / MySQL
- Database client

## SQL Concepts Practiced

- SELECT
- WHERE
- ORDER BY
- JOIN
- Filtering records
- Reading query results

## Skills Practiced

- Basic SQL
- Database investigation
- Application troubleshooting
- Data verification
- Technical support documentation

## What I Learned

This lab helped me understand how SQL can be used as a troubleshooting tool in Application Support. The focus was on querying and verifying information to collect evidence and better understand a reported issue.
