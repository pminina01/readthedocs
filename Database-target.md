Writes log messages to the database using an ADO.NET provider. The database operation is always executed outside of a transaction.

Supported in .NET, Compact Framework and Mono
##Configuration Syntax
```xml
<targets>
  <target xsi:type="Database"
          name="String"
          dbUserName="Layout"
          dbProvider="String"
          *useTransactions="Boolean"
          connectionStringName="String"
          connectionString="Layout"
          keepConnection="Boolean"
          dbDatabase="Layout"
          dbPassword="Layout"
          dbHost="Layout"
          installConnectionString="Layout"
          commandText="Layout">
    <install-command commandType="Enum" connectionString="Layout" ignoreFailures="Boolean"
                 text="Layout"/><!-- repeated -->
    <uninstall-command commandType="Enum" connectionString="Layout" ignoreFailures="Boolean"
                   text="Layout"/><!-- repeated -->
    <parameter layout="Layout" name="String" precision="Byte"
         scale="Byte" size="Integer"/><!-- repeated -->
  </target>
</targets>
```
Read more about using the [Configuration File](Configuration file).
##Parameters
###General Options
_name_ - Name of the target.
###Connection Options
_dbUserName_ - Database user name. If the ConnectionString is not provided this value will be used to construct the "User ID=" part of the connection string. [Layout](Layout)  
_dbProvider_ - Name of the database provider. Required. Default: sqlserver  
The parameter name should be a provider invariant name as registered in machine.config or app.config. Common values are:
* System.Data.SqlClient -
* System.Data.SqlServerCe.3.5 -
* System.Data.OracleClient - (deprecated in .NET Framework 4)
* Oracle.DataAccess.Client -
* System.Data.SQLite -
* Npgsql -
* MySql.Data.MySqlClient -

(Note that provider invariant names are not supported on .NET Compact Framework). Alternatively the parameter value can be be a fully qualified name of the provider connection type (class implementing IDbConnection) or one of the following tokens:
* sqlserver, mssql, microsoft or msde - SQL Server Data Provider
* oledb - OLEDB Data Provider
* odbc - ODBC Data Provider

_useTransactions_ - This option was removed in NLog 4.0 because the logging code always runs outside of transaction. This ensures that the log gets written to the database if you rollback the main transaction because of an error and want to log the error.

_connectionStringName_ - Name of the connection string (as specified in .  
> This parameter is not supported in:
> * NLog v1.0 for .NET Compact Framework 1.0
> * NLog v1.0 for .NET Compact Framework 2.0
> * NLog v1.0 for .NET Framework 1.0
> * NLog v1.0 for .NET Framework 1.1
> * NLog v1.0 for .NET Framework 2.0
> * NLog v2.0 for .NET Compact Framework 2.0
> * NLog v2.0 for .NET Compact Framework 3.5

_connectionString_ - Connection string. When provided, it overrides the values specified in DBHost, DBUserName, DBPassword, DBDatabase and DBProvider. [Layout](Layout)  
_keepConnection_ - Indicates whether to keep the database connection open between the log events. [Boolean](Data types) Default: `false`  
_dbDatabase_ - Database name. If the ConnectionString is not provided this value will be used to construct the "Database=" part of the connection string. [Layout](Data types)  
_dbPassword_ - Database password. If the ConnectionString is not provided this value will be used to construct the "Password=" part of the connection string. [Layout](Data types)  
_dbHost_ - Database host name. If the ConnectionString is not provided this value will be used to construct the "Server=" part of the connection string. [Layout](Data types)  
###Installation Options
_installDdlCommands_ - The installation DDL commands. [Collection](Data types)  
Each collection item is represented by \<install-command /> element with the following attributes:
  * _commandType_ - Type of the command. Required. Default: 1  
Possible values:
    * StoredProcedure -
    * TableDirect -
    * Text -
  * _connectionString_ - Connection string to run the command against. If not provided, connection string from the target is used. [Layout](Data types)  
  * _ignoreFailures_ - Indicates whether to ignore failures. [Boolean](Data types)  
  * _parameters_ - The collection of parameters. Each parameter contains a mapping between NLog layout and a database named or positional parameter. [Collection](Data types)  
Each collection item is represented by <parameter /> element with the following attributes:
    * _layout_ - Layout that should be use to calcuate the value for the parameter. [Layout](Data types) Required.
    * _name_ - Database parameter name. Required.
    * _precision_ - Database parameter precision. [Byte](Data types) Default: 0
    * _scale_ - Database parameter scale. [Byte](Data types) Default: 0
    * _size_ - Database parameter size. [Integer](Data types) Default: 0
    * _text_ - Command text. [Layout](Data types) Required.  

      > This parameter is not supported in:
      > * NLog v1.0 for .NET Compact Framework 1.0
      > * NLog v1.0 for .NET Compact Framework 2.0
      > * NLog v1.0 for .NET Framework 1.0
      > * NLog v1.0 for .NET Framework 1.1
      > * NLog v1.0 for .NET Framework 2.0
    * _installConnectionString_ - Connection string using for installation and uninstallation. If not provided, regular ConnectionString is being used. [Layout](Layout)  

      > This parameter is not supported in:
      > * NLog v1.0 for .NET Compact Framework 1.0
      > * NLog v1.0 for .NET Compact Framework 2.0
      > * NLog v1.0 for .NET Framework 1.0
      > * NLog v1.0 for .NET Framework 1.1
      > * NLog v1.0 for .NET Framework 2.0
    * _uninstallDdlCommands_ - The uninstallation DDL commands. [Collection](Data types)  
Each collection item is represented by \<uninstall-command /> element with the following attributes:
      * _commandType_ - Type of the command. Required. Default: 1  
Possible values:
        * StoredProcedure -
        * TableDirect -
        * Text -
      * _connectionString_ - Connection string to run the command against. If not provided, connection string from the target is used. [Layout](Layout)  
      * _ignoreFailures_ - Indicates whether to ignore failures. [Boolean](Layout)  
      * _parameters_ - The collection of parameters. Each parameter contains a mapping between NLog layout and a database named or positional parameter. [Collection](Layout)  
Each collection item is represented by \<parameter /> element with the following attributes:
        * _layout_ - Layout that should be use to calcuate the value for the parameter. [Layout](Layout) Required.
        * _name_ - Database parameter name. Required.
        * _precision_ - Database parameter precision. [Byte](Data types) Default: 0
        * _scale_ - Database parameter scale. [Byte](Data types) Default: 0
        * _size_ - Database parameter size. [Integer](Data types) Default: 0
        * _text_ - Command text. [Layout](Data types) Required.

        > This parameter is not supported in
        > * NLog v1.0 for .NET Compact Framework 1.0
        > * NLog v1.0 for .NET Compact Framework 2.0
        > * NLog v1.0 for .NET Framework 1.0
        > * NLog v1.0 for .NET Framework 1.1
        > * NLog v1.0 for .NET Framework 2.0

###SQL Statement
_commandText_ - Text of the SQL command to be run on each log level. [Layout](Data types) Required.  
Typically this is a SQL INSERT statement or a stored procedure call. It should use the database-specific parameters (marked as @parameter for SQL server or :parameter for Oracle, other data providers have their own notation) and not the layout renderers, because the latter is prone to SQL injection attacks. The layout renderers should be specified as \<parameter /> elements instead.

_parameters_ - The collection of parameters. Each parameter contains a mapping between NLog layout and a database named or positional parameter. [Collection](Data types)  
Each collection item is represented by \<parameter /> element with the following attributes:
* _layout_ - Layout that should be use to calcuate the value for the parameter. [Layout](Data types) Required.  
* _name_ - Database parameter name. Required.
* _precision_ - Database parameter precision. [Byte](Data types) Default: 0
* _scale_ - Database parameter scale. [Byte](Data types) Default: 0
* _size_ - Database parameter size. [Integer](Data types) Default: 0