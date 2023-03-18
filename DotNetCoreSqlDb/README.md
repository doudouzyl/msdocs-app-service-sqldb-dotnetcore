# Project Name
Tutorial: Deploy an ASP.NET Core and Azure SQL Database app to Azure App Service - ASP.NET Core TODO List Sample App with MySQL 8.0 Flexible Server

## Changes
1. Updated to use .NET 7
2. Updated to use MySQL 8.0 Flexible Server
3. Use the following packages:
    <PackageReference Include="Microsoft.EntityFrameworkCore" Version="7.0.4" />
    <PackageReference Include="Microsoft.EntityFrameworkCore.Design" Version="7.0.4">
    <PackageReference Include="Microsoft.EntityFrameworkCore.Tools" Version="7.0.4">
    <PackageReference Include="Pomelo.EntityFrameworkCore.MySql" Version="7.0.0" />
4. Build the project on a VM with access to MySQL server and regenerate the migration classes.

### Configuration
AZURE_MYSQL_CONNECTIONSTRING - will be used for MySQL db server connection

### Installation
Tested on Ubuntu

```bash
dotnet build --configuration Release
dotnet publish -c Release
dotnet tool install --global dotnet-ef
dotnet ef migrations add InitialCreate
```

### GitHub actions for generating migration boundle 

      - name: dotnet install ef
        run: dotnet tool install -g dotnet-ef

      - name: start mysql
        run: sudo systemctl start mysql.service

      - name: dotnet generate migration
        run: dotnet ef migrations bundle --verbose --self-contained -p DotNetCoreSqlDb/DotNetCoreSqlDb.csproj -o ${{env.DOTNET_ROOT}}/myapp/migrate

### Misc
To connect your MySQL 8.0 Flexible Server using MySQL client(from a VM)

```bash
 mysql -h xxx.mysql.database.azure.com -u xxxUserNamexxx -p --ssl-mode=REQUIRED --ssl-ca=/home/azureuser/<your_downloaded_cert>.pem
```
