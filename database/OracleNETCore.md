# Oracle & NET Core 
Hints & tips on using Oracle with .NET Core

## Overview and Installation 
At last, a new .NET Core provider is available:  
[Docs](https://docs.oracle.com/en/database/oracle/oracle-data-access-components/18.3/odpnt/release_changes.html#GUID-7EDAEAB4-55C9-4D59-AAC8-D37EECB11395)

And you can download the library using NuGet in Visual Studio  
**Oracle.ManagedDataAccess.Core**

There are no namespace changes, the NETCore version uses the same namespaces as standard Managed version, just a different assembly.  
**Oracle.ManagedDataAccess.Client**  
**Oracle.ManagedDataAccess.Types**  

## Reading data that contains Nulls
This is a pain. To read a string we use a line of code like this:  
```
string name = reader.GetString("name");
```

however, this will cause an exception if the value is null. So we must do this:  
```
if(!reader.IsDBNull("name"))  
{  
  string name = reader.GetString("name");  
}
```

messy. One solution is to write an OracleDataReader Extension class:  
```
public static class OracleDataReaderExtension  
{  
  public static string GetStringNullable(this IDataReader r, string columnName)  
  {  
      var value = r.GetValue(r.GetOrdinal(columnName));  
      if (value is DBNull)  
          return null;  
      return Convert.ToString(value);  
  }
```

then we can write:  
```
string name = reader.GetStringNullable("name");
```

## Oracle Features 
The .NET Core implementation...
