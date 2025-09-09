# Overview of AI tooling and more for Microsoft

| Link | Notes |
| --- | --- |
| [Listing of LLM](https://en.wikipedia.org/wiki/List_of_large_language_models) | good for keeping up to date | 
| [AI Foundry Portal](https://ai.azure.com/) | seperate to the Azure |


**Terminology**

| TLA | Term | Description | Example |
| ---- |  ---- | ---- | ---- |
| SLM | Small Language Model | optimized for specific scenarios. Cost effective / speedy. low spec devices | |
| LLM | Large Language Model | Cruch large quantities of data to get the average. deep reasoning, complex content | |
| | Multi Model model | prompts & responses can includes images, speeach |
| RAG | Retrieval Augmented Generation | access right data from your database | |
| | GenAI | original responses to natural language prompts. uses LM's to respond to prompts | |
| | Agents | GenAi that can respond to user input or assess situations autonomously | CoPilot |
| | Computer Vision <sup>1</sup> | process images, videos etc. | e.g. Scan grocery instead of barcode |
| NPL | Natural Processing Language <sup>2</sup> | process natural language | e.g social media entry -> categorize |
|  | Speech <sup>3</sup> | ability to recognise and synthesize speech | e.g alexa |
| | Information Extraction | ability to use <sup>1</sup>,<sup>2</sup> and <sup>3</sup> to extract information | 
| | Descision Support | ability to use historic and learned correlations to make predications |

## LLM Background 
*Transformer Models* - process words individually and in parallel. use *attention* and *positional encoding*  
Models: 1000's to choose from. [huggingface](https://huggingface.co/models), [github](https://github.com/marketplace/models-github) [azure](https://ai.azure.com/explore/models?tid=aef7d964-ee79-491b-b95e-ebf0e1b9db8c)  
Choice
- LLM v SLM  
- Modality, task, tool

## Azure AI Services

| Service | Description | Notes |
| ---- |  ---- | ---- |
| Azure Open AI | use OpenAI generative models | |
| Azure AI Doc Intelligence | Extract fields from documents |
| Azure AI Search | Uses other AI Services to extract content and create search able index | 

Single Azure resource for using multiple services
| Service | Description | Notes |
| ---- |  ---- | ---- |
| Azure AI Services | works with speech, face, docs, vision etc  | |
| Azure AI Foundry | same as above plus OpenAI, Content Understanding, Content Safety | no custom vision |

## Tools 
**Azure AI Foundry**
Portal and SDK.  
*Hub based projects* - AIF & managed compute, storage account, keyvault  
**GitHub CoPilot** - AI for coding  
**Foundry SDK** - SDK for founrdy projects, use additional service sdks   
**Foundry Models API** - for gen ai endpoints  
**Open AI in Foundry Models API** - build OpenAI chat bots  
**AI Services SDKs** - libs for multiples frameworks/languages to consume the Rest Services  
**AI Founrdy Agent Service** - accessed via SDK used to build comprehensive agent solutions

## AI Foundry 
2 azure resources created  
- *azure ai foundry* resource - includes connections, models  
- *azure ai foundry project* - includes project specific resources   

Use the endpoints & keys to access:  
- the project  
- the azure ai services  
- the OpenAI foundry models  



## SQL
overview of tooling in the [sql documentation](https://learn.microsoft.com/en-us/sql/sql-server/ai-artificial-intelligence-intelligent-applications?view=sql-server-ver17)