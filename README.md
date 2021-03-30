# node-couchbase-compat-server
This is a NODE.JS Server Offering mysql, redis Compatible Protocols for Couchbase so you can use Couchbase as backend for all Applications.


## Why?
The Idea Behind this was and maybe is to translate all kind of Protocols to Couchbase N1QL Querys. This allows then to use Couchbase as a Backend without Modification to the existing Application.

While i did not focus on this effort so much 2 companys did create mysql drivers that translate to diffrent N1QL schemas

I think it is at present the most easy part to modify Application DB Layers. The Idea of a Driver that does the Translation is maybe not as performant as a translation server.

Pro: Translation Server
- Can Still Speak the Original Protocol and can Mirror into 2 diffrent databases to migrate data smooth
- is able to Offer diffrent ApiÄs Like for example done With Oracle Graal which is able to Compile code to get used inside Oracle DB
- Can Shard diffrent Databases.

Pro: Adapter
- No Additional Server Costs.
- 


# a  MYSQL, REDIS, COUCHBASE, Compatible  server using Couchbase as backend.

Reference of joins as puts and insert and delet by key is simply
http://www.sitepoint.com/understanding-sql-joins-mysql-database/

~~~
MYSQL TABLES:

TableName Clients:
|ID|NAME|LASTNAME|TEL|
-----------------------
|1|Frank|Legende|00|
|2|Frank|Legende|00|

TableName Logins:
|ID|LOGIN|PASSWORD|
-----------------------
|11|frank@legend.org|Legende|
|22|Frank@neverdie.org|Legende|

now a mysql join statment will retrive a document with |ID|NAME|LASTNAME |TEL| LOGIN|PASSWORD|




to enable use statment and that we need the ability to log some values by reqest so no real problem


query all type mysql_table where db_name & table_name (All Results of a mysql table)

USE db_name
single entry SELECT * FROM USERS WHERE ID=1
query type mysql_table db_name table_name where filds.id = 1 


// define a fild constrained into the schema so we can maintain delets and changes
// if fild course that contains number 5 

// This if you alter table users with a reference for table course we need to modify table course and add a info that we added that constraint to it so we leave constrained in it
// then we will always check on write or delet or modify if the constraints are in takt that means that the constained object from user table is in courses table
// so that a delet on this table 
ALTER TABLE `user`
ADD CONSTRAINT `FK_course`
FOREIGN KEY (`course`) REFERENCES `course` (`id`)
ON UPDATE CASCADE;

enters into refenced table schema reference fild to altered table with forgein key fild and adds info to altered table that refences this constained by add constained

key: mysql_#DB_#TABLE {
  db: 'dbname',
  table: 'tablenamee'
  schema: [
    id: smallint(5) unsigned NOT NULL AUTO_INCREMENT,
    name: varchar(50) NOT NULL,
    PRIMARY_KEY: id
    ],
  constrained: [ 'FK_course' ]
}

check id for smallint(5), notnull, AUTO_INCREMENT, PRIMARY_KEY and Add document
check name for varchar(50), and notnull and Add it
create new key based on PRIMARY_KEY :) 

read db table key is no problem because we can simply retrive the document and return filds its a refdoc

on select from we can return wished filds or return wished filds from a set of documents no problem at all couchbase is amazing 

key: mysql_#DB_#TABLE_#UUIDFILD { 
  type:mysql_table
  db_name: name
  table_name:users
  filds: [
    id: "1"
    name: "Frank"
  ]


}




we get a write request for db and table and apply mysql_#DB_#TABLE.schema against it then return mysql like error or success msg
we get read select request for db table and will do translate that to a n1ql query against the right ids

