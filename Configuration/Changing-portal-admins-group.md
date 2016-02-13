## Update portal admins group external id
* Update value of ```portal-admins-group``` configuration parameter in ```Portal_Config``` table. This value should be Group DN in case of LDAP and ID in case of DB.
* Login to portal with credentials of a portal administrator.
* Update permissions for ```Admin``` site and add new portal admins group to ```Manager``` role.
* Logout and login with a user credentials who is member of new portal admins group. Remove old portal admins group from ```Manager``` role of ```Admin``` site. 