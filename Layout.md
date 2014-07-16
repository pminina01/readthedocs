<target xsi:type="Database"
            name="Base"
            dbUserName="Operator"
            dbProvider="System.Data.SqlClient"
            dbDatabase="ControlTime"
            dbPassword="Operator"
            dbHost="A-YAKSHIN"
            commandText="INSERT INTO [dbo].[Logs](Date, Level, Logger, Message) VALUES (${longdate}, ${uppercase:${level}}, ${logger}, ${message});"
            />