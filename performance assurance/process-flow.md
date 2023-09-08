# Process Flow

Need to outline the process that is taken in the development and execution of the Performance Assurance utility.

- Inventory and cleanup files/folders
- Outline development strategy
  - branch usage
  - steps, jobs, stages, pipelines
- Show execution flow
  - how blob storage is used
  - how ADF kicks off and triggers ADO
  - how pipeline conditions work
- Create config map to outline manifest modifying


** Create App Registration
** Give access to ACR from SCRSFD app registration

## Azure Data Factory

https://www.youtube.com/watch?v=qvyylliksdE

- Create an Azure Data Factory Resource
- Load ADF Studio
  - Create a new pipeline
  - Add a "Move and Transform - Copy Data" activity
  - 