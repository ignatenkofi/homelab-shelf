## Migrating from RouterOS v6 

When you upgrade your User Manager router from RouterOS v6 to the v7 the new User Manager will work with new database files and configuration. To continue using the old user, router, profile, etc. configuration you must manually execute the migrate command. To do so you must have files from the old User Manager server folder "user-manager" present. The folder can be renamed, but all the contents from the old installation must be transferred to the new v7 installation (you can move the old configuration from one router to another router with v7, you must copy "user-manager" folder). After that, all you need to do is execute this command - "/user-manager/database/migrate-legacy-db database-path=<path_to_old_user_manager_folder>". 

The import process will try to convert such configuration - users, profiles, user-profiles, limitations, profile-limitations, user-counters, routers, and sessions.
