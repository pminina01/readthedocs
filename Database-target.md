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

Example of using a fully qualified name with Mono.Data.Sqlite
 
    dbProvider="Mono.Data.Sqlite.SqliteConnection, Mono.Data.Sqlite, Version=4.0.0.0, Culture=neutral, PublicKeyToken=0738eb9f132ed756"

_useTransactions_ - This option was removed in NLog 4.0 because the logging code always runs outside of transaction. This ensures that the log gets written to the database if you rollback the main transaction because of an error and want to log the error.

_connectionStringName_ - Name of the connection string. The ProviderName of the connectionstring will be used to determine the SQL type. Since NLog 4.3 this  ProviderName attribute isn't required anymore and the `dbProvider` will be used as fallback.


_connectionString_ - Connection string. When provided, it overrides the values specified in DBHost, DBUserName, DBPassword, DBDatabase and DBProvider. [Layout](Layout)  

_keepConnection_ - Indicates whether to keep the database connection open between the log events. [Boolean](Data types) Default: `false`  

_dbDatabase_ - Database name. If the ConnectionString is not provided this value will be used to construct the "Database=" part of the connection string. [Layout](Data types)  

_dbPassword_ - Database password. If the ConnectionString is not provided this value will be used to construct the "Password=" part of the connection string. [Layout](Data types)  

_dbHost_ - Database host name. If the ConnectionString is not provided this value will be used to construct the "Server=" part of the connection string. [Layout](Data types)  

###Installation Options
_installDdlCommands_ - The installation DDL commands. [Collection](Data types)  
Each collection item is represented by \<install-command /> element with the following attributes:
  * _commandType_ - Type of the command. Required. Default: `text`  
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
    * _installConnectionString_ - Connection string using for installation and uninstallation. If not provided, regular ConnectionString is being used. [Layout](Layout)  
    * _uninstallDdlCommands_ - The uninstallation DDL commands. [Collection](Data types)  
Each collection item is represented by \<uninstall-command /> element with the following attributes:
      * _commandType_ - Type of the command. Required. Default: `text` 
Possible values:
        * `StoredProcedure` - `commandText` is the stored procedure name.
        * `TableDirect` -
        * `Text` - regular query
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

##Example Configurations

### SQL Server and ASP.NET Example Configuration
```xml
<target name="database" xsi:type="Database">
  <!--
  Remarks:
    The appsetting layouts require the NLog.Extended assembly.
    The aspnet-* layouts require the NLog.Web assembly.
    The Application value is determined by an AppName appSetting in Web.config.
    The "NLogDb" connection string determines the database that NLog write to.
    The create dbo.Log script in the comment below must be manually executed.
  -->

  <connectionStringName>NLogDb</connectionStringName>

  <!--
  Script for creating the dbo.Log table.
      
  SET ANSI_NULLS ON
  SET QUOTED_IDENTIFIER ON
  CREATE TABLE [dbo].[Log] (
	  [Id] [int] IDENTITY(1,1) NOT NULL,
	  [Application] [nvarchar](50) NOT NULL,
	  [Logged] [datetime] NOT NULL,
	  [Level] [nvarchar](50) NOT NULL,
	  [Message] [nvarchar](max) NOT NULL,
	  [UserName] [nvarchar](250) NULL,
	  [ServerName] [nvarchar](max) NULL,
	  [Port] [nvarchar](max) NULL,
	  [Url] [nvarchar](max) NULL,
	  [Https] [bit] NULL,
	  [ServerAddress] [nvarchar](100) NULL,
	  [RemoteAddress] [nvarchar](100) NULL,
	  [Logger] [nvarchar](250) NULL,
	  [Callsite] [nvarchar](max) NULL,
	  [Exception] [nvarchar](max) NULL,
    CONSTRAINT [PK_dbo.Log] PRIMARY KEY CLUSTERED ([Id] ASC)
      WITH (PAD_INDEX  = OFF, STATISTICS_NORECOMPUTE  = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS  = ON, ALLOW_PAGE_LOCKS  = ON) ON [PRIMARY]
  ) ON [PRIMARY]
  -->
      
  <commandText>
    insert into dbo.Log (
      Application, Logged, Level, Message,
      Username,
      ServerName, Port, Url, Https,
      ServerAddress, RemoteAddress,
      Logger, CallSite, Exception
    ) values (
      @Application, @Logged, @Level, @Message,
      @Username,
      @ServerName, @Port, @Url, @Https,
      @ServerAddress, @RemoteAddress,
      @Logger, @Callsite, @Exception
    );
  </commandText>

  <parameter name="@application" layout="${appsetting:name=AppName:default=Unknown\: set AppName in appSettings}" />
  <parameter name="@logged" layout="${date}" />
  <parameter name="@level" layout="${level}" />
  <parameter name="@message" layout="${message}" />

  <parameter name="@username" layout="${identity}" />

  <parameter name="@serverName" layout="${aspnet-request:serverVariable=SERVER_NAME}" />
  <parameter name="@port" layout="${aspnet-request:serverVariable=SERVER_PORT}" />
  <parameter name="@url" layout="${aspnet-request:serverVariable=HTTP_URL}" />
  <parameter name="@https" layout="${when:inner=1:when='${aspnet-request:serverVariable=HTTPS}' == 'on'}${when:inner=0:when='${aspnet-request:serverVariable=HTTPS}' != 'on'}" />

  <parameter name="@serverAddress" layout="${aspnet-request:serverVariable=LOCAL_ADDR}" />
  <parameter name="@remoteAddress" layout="${aspnet-request:serverVariable=REMOTE_ADDR}:${aspnet-request:serverVariable=REMOTE_PORT}" />

  <parameter name="@logger" layout="${logger}" />
  <parameter name="@callSite" layout="${callsite}" />
  <parameter name="@exception" layout="${exception:tostring}" />
</target>
```

### ASP.NET and SQL Server using a stored procedure

This approach keeps the NLog.config file simpler, and helps confine 
database logic to the database.

#### NLog target configuration

```xml
<target name="db"
        xsi:type="Database"
        connectionStringName="NLogConn"
        commandType="StoredProcedure"
        commandText="[dbo].[NLog_AddEntry_p]"
        >
  <parameter name="@machineName"    layout="${machinename}" />
  <parameter name="@siteName"       layout="${iis-site-name}" />
  <parameter name="@logged"         layout="${date}" />
  <parameter name="@level"          layout="${level}" />
  <parameter name="@username"       layout="${aspnet-user-identity}" />
  <parameter name="@message"        layout="${message}" />
  <parameter name="@logger"         layout="${logger}" />
  <parameter name="@properties"     layout="${all-event-properties:separator=|}" />
  <parameter name="@serverName"     layout="${aspnet-request:serverVariable=SERVER_NAME}" />
  <parameter name="@port"           layout="${aspnet-request:serverVariable=SERVER_PORT}" />
  <parameter name="@url"            layout="${aspnet-request:serverVariable=HTTP_URL}" />
  <parameter name="@https"          layout="${when:inner=1:when='${aspnet-request:serverVariable=HTTPS}' == 'on'}${when:inner=0:when='${aspnet-request:serverVariable=HTTPS}' != 'on'}" />
  <parameter name="@serverAddress"  layout="${aspnet-request:serverVariable=LOCAL_ADDR}" />
  <parameter name="@remoteAddress"  layout="${aspnet-request:serverVariable=REMOTE_ADDR}:${aspnet-request:serverVariable=REMOTE_PORT}" />
  <parameter name="@callSite"       layout="${callsite}" />
  <parameter name="@exception"      layout="${exception:tostring}" />
</target>

<!--
  Notes:

  - Some of these layout renderers require a reference to NLog.Web. 
    (http://nuget.org/List/Packages/NLog.Web)

  - If the connection string was created with Visual Studio's Settings dialog
    then its name may be prefixed with a namespace like "<project>.Settings.Properties.*".
    If so be sure to include the entire name (with the namespace).
-->
```

#### SQL scripts to set up the database objects

Remember to grant permissions on the database objects so that the website can execute the stored procedure.

```sql
CREATE TABLE [dbo].[NLog] (
   [ID] [int] IDENTITY(1,1) NOT NULL,
   [MachineName] [nvarchar](200) NULL,
   [SiteName] [nvarchar](200) NOT NULL,
   [Logged] [datetime] NOT NULL,
   [Level] [varchar](5) NOT NULL,
   [UserName] [nvarchar](200) NULL,
   [Message] [nvarchar](max) NOT NULL,
   [Logger] [nvarchar](300) NULL,
   [Properties] [nvarchar](max) NULL,
   [ServerName] [nvarchar](200) NULL,
   [Port] [nvarchar](100) NULL,
   [Url] [nvarchar](2000) NULL,
   [Https] [bit] NULL,
   [ServerAddress] [nvarchar](100) NULL,
   [RemoteAddress] [nvarchar](100) NULL,
   [Callsite] [nvarchar](300) NULL,
   [Exception] [nvarchar](max) NULL,
 CONSTRAINT [PK_dbo.Log] PRIMARY KEY CLUSTERED ([ID] ASC) 
   WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY];

CREATE PROCEDURE [dbo].[NLog_AddEntry_p] (
  @machineName nvarchar(200),
  @siteName nvarchar(200),
  @logged datetime,
  @level varchar(5),
  @userName nvarchar(200),
  @message nvarchar(max),
  @logger nvarchar(300),
  @properties nvarchar(max),
  @serverName nvarchar(200),
  @port nvarchar(100),
  @url nvarchar(2000),
  @https bit,
  @serverAddress nvarchar(100),
  @remoteAddress nvarchar(100),
  @callSite nvarchar(300),
  @exception nvarchar(max)
) AS
BEGIN
  INSERT INTO [dbo].[NLog] (
    [MachineName],
    [SiteName],
    [Logged],
    [Level],
    [UserName],
    [Message],
    [Logger],
    [Properties],
    [ServerName],
    [Port],
    [Url],
    [Https],
    [ServerAddress],
    [RemoteAddress],
    [CallSite],
    [Exception]
  ) VALUES (
    @machineName,
    @siteName,
    @logged,
    @level,
    @userName,
    @message,
    @logger,
    @properties,
    @serverName,
    @port,
    @url,
    @https,
    @serverAddress,
    @remoteAddress,
    @callSite,
    @exception
  );
END
```
