# Creating a DbContext
This is quite easy when you know how. This example show how to setup connection to a MySql instance.

```json
{ "date": "2019-08-17", "dotnetcoreversion": "3.0.100-preview8-013656", "os": "Windows 10 Pro 1903 - 18362.295" }
```

I like to separate database related code into a separate namespace, or maybe even a separate project.
Under you see the files you must configure. Whenever there are three dots (...) you probably have more content yourself. Whenever a name starts with "My" you can of course make names that suit your needs.

```cs
# /DataStore/Entity/MyEntity.cs - Create your entities
namespace x.DataStore.Entity
{
  public class MyEntity
  {
    public int Id { get; set; }
    ...
  }
}

# /DataStore/MyDbContext.cs - Define your data context with your database entities
namespace x.DataStore
{
  public class MyDbContext : DbContext
  {
    public MyDbContext(DbContextOptions<MyDbContext> options) : base (options)
    { }
    
    public DbSet<MyEntity> MyEntities { get; set; }
    ...
  }
}

# /appsettings.json - Define host, database, username and password for your database instance
{
  ...
  "ConnectionStrings": {
    "MyConnectionStrings": "server=localhost;database=Mydatabase;user=Myuser;password=Mypassword"
  }
}

# /Startup.cs - Enable the data context by configuring as a service, using appsettings.
...
  public void ConfigureServices(IServiceCollection services)
  {
    ...
    services.AddDbContext<MyDbContext>(optionsBuilder =>
      optionsBuilder.UseMySql(Configuration.GetConnectionString("MyConnectionString"))
    );
    ...
  }
...
```
