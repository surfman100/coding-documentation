# Entity Framework
## Setup
Add a reference to Microsoft.EntityFrameworkCore.SQLServer

## Add a Context
A simmple context
```
using Microsoft.EntityFrameworkCore;
using Microsoft.Extensions.Logging;

public class MyDBContext : DbContext
{
    public MyDBContext(DbContextOptions<MyDBContext> options)
        : base(options)
    {
    }
    
    // prevent SQL statement entries on console window
    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        base.OnConfiguring(optionsBuilder);

        optionsBuilder.UseLoggerFactory(LoggerFactory.Create(builder =>
        {
            builder.AddFilter(_ => false);
        }));
    }
    
    public DbSet<MyInvoiceClass> Invoices { get; set; }

    public DbSet<AnotherClass> NotATable { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<NotATable>().ToSqlQuery(_someQuery_);
    }
}
```

## Data Annotations
Try to have an ID field on your table.

```
using System.ComponentModel.DataAnnotations;
using System.ComponentModel.DataAnnotations.Schema;


[Table("someothername")]
public class MyInvoiceClass
{
    public int ID { get; set; }

    [Column(TypeName = "decimal(20,2)")]
    public decimal? InvoiceAmount { get; set; }
}
```

## Startup code
add the context in service registration
```
    .AddDbContext<MigrationDBContext>(options => options.UseSqlServer(configuration["DaeMigraton"]))
```