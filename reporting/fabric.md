# Fabric 
An all-in-one analytics solution i.e. 
- data integrations 
- storage 
- data warehousing 
- data engineering 
- business intelligence 
- data science 

[Fabric Portal](https://app.fabric.microsoft.com/home?experience=fabric-developer) 

single product with references / re-badge of:
- PowerBI
- Datafactory
- Purview
highly scalable/performant

## Terminology 
| Item	| **Data warehouse** | **Lakehouse** | **Power BI Datamart** | 
| --- | --- | --- | --- |
| Data volume | 	Unlimited | Unlimited |	Up to 100 GB |
| Type of data | Structured | Unstructured, semi-structured, structured |	Structured |
| Primary developer persona	| Data warehouse developer, SQL engineer | Data engineer, data scientist | Citizen data analyst |
| Primary developer skill set |	SQL	| Spark (Scala, PySpark, Spark SQL, R) |	No code (Power Query), SQL |
| ETL |	Data Pipelines, Dataflows Gen2, SQL | Data Pipelines, Dataflows Gen2, Notebooks, Spark Job Definitions | Dataflows |
| Languages to work with | T-SQL, Spark | Spark (Scala, PySpark, Spark SQL, R) | Dataflows, T-SQL |
| SQL Endpoint | Read and Write | Read-only	| Read-only |
| Primary development interface | SQL scripts |	Spark notebooks, Spark job definitions |	Power BI |
| Licenses | Fabric Capacity	| Fabric Capacity	| Fabric Capacity, Power BI Premium, PPU |

**OneLake** storage layer in fabric  
**Delta lake format** fabric standardise on this so need need to copy data  


## Data Lake / Lakehouse 
**Move/Write** your data here using pipelines, dataflows, notebooks, spark jobs 
**Read** datra using browser Lakehouse Explorer & SQL endpoint
- classify it / sensitivity label  
- endorse it 