# AutoMigration-Asp.net-Core-
In startup.cs Place the following codes. And run the program. 

Put a debugger on the using block in the configure method for test. It will update the database according to the database context. It will be good if the cood is placed in the #If Debug mode. 
```csharp
// This method gets called by the runtime. Use this method to add services to the container.
public void ConfigureServices(IServiceCollection services)
{
    var connectionString = Configuration.GetConnectionString("MebCbsConection");
    var migrationsAssembly = typeof(Startup).GetTypeInfo().Assembly.GetName().Name;
    ...
}

// This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    using (var scope = app.ApplicationServices.GetService<IServiceScopeFactory>().CreateScope())
    {
        scope.ServiceProvider.GetRequiredService<MebCbsAnkaContext>().Database.Migrate();
       // Other DB context can be placed here

    }
    ...
}

```
