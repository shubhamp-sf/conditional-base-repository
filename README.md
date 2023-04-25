The requirement is to give users of sourceloop service a way to switch from Juggler to Sequelize or vice versa for underlying crud repositories provided by the service.

Technically this implies that current crud repositories in the services extending `DefaultCrudRepository` should be switchable to `SequelizeCrudRepository`.

To achieve this all the repositories in sourceloop services will extend from a factory function `ConditionalCrudRepository()` which checks a flag from `process.env` and returns the `SequelizeCrudRepository` if specified or the default one otherwise.

<img src="https://user-images.githubusercontent.com/110156023/234196953-2f71217d-d84b-4644-b1c7-a017a9cfebac.png" width="800">

Operationally this works well, but the end application using sourceloop services might extend the crud repository class that will need the proper type of the Exported repository based on the condition specified. 

By default when projects using this flag need to extend any of the repositories of the service. They will have the type set as DefaultCrudRepository which limits us in case there is extra stuff that SequelizeCRUDRepository provides. So to tackle this Project code will have to keep a d.ts file.(which can be placed via postinstall script).

That looks something like this:
<img src="https://user-images.githubusercontent.com/110156023/234196771-0e8dacb1-73be-48b8-9733-8986720037b5.png" width="800">
