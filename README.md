Workout
==========================

Giving Neo4j 2.2 a workout with Gatling 2.1

Install Neo4j and maven.

Create some data.

    WITH ["Jennifer","Michelle","Tanya","Julie","Christie","Sophie","Amanda","Khloe","Sarah","Kaylee"] AS names
    FOREACH (r IN range(0,10000000) | CREATE (:User {username:names[r % size(names)]+r}))

    MATCH (u1:User),(u2:User)
    WITH u1,u2
    LIMIT 500000000
    WHERE rand() < 0.1
    CREATE (u1)-[:FRIENDS]->(u2);

$ mvn gatling:execute -Dgatling.simulationClass=GetFriends

Add an index.

    CREATE INDEX ON :User(username)

$ mvn gatling:execute -Dgatling.simulationClass=GetFriends

See [blog post](http://wp.me/p26jdv-Ja) for more details.
