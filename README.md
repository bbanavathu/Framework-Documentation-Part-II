# Framework-Documentation-Part-II
#### This part is dedicated to explain the different **Classes** of Surround.
Classes run a means of bundling data and functionality together. Creating a new class creates a new type of object, allowing new instances of that type to be made. Each class instance can have attributes attached to it for maintaining its state. Class instances can also have methods defined by its class for modifying its state.

## Let us see some of the classes 
1.  class Config(Mapping):
2.  class LinterStage(Stage):
3.  class Stage(ABC):
4.  class Frozen(): 

### class Config(Mapping): 

This class helps in Identifying the different paths for output, data, models, Importing the location.

**The main features of mapping include:**

1.	creating continuous return series for Futures instruments
2.	creating time series of percentage allocations to tradeable contracts
3.	creating instrument trade lists

Use `models` paths to maintain consistency

class Config(Mapping):

    def __init__(self, project_root=None):
        self._storage = self.__load_defaults()

        # Set framework paths
        if project_root:
            self._storage["project_root"] = project_root
            self._storage["output_path"] = os.path.join(project_root, "output")
            self._storage["data_path"] = os.path.join(project_root, "data")
            self._storage["models_path"] = os.path.join(project_root, "models")
            
### class LinterStage(Stage):

This class helps in verifying the quality of the code and analyse source code for potential erros,
lint is a tool which is used to mark the source code with some suspicious and non-structural.

**These classes Add support for the Running Project specific tasks**

1. For the Lint process to execute and check for errors and add warning if bugs are found,

       class LinterStage(Stage):
  
2. To check the Data in the linter stage
    
       class CheckData(LinterStage):
         
3. To check the Surround project files
 
       class CheckFiles(LinterStage):
         
4. To check the Directories and validating Surround's directory structure  

       class CheckDirectories(LinterStage):
         
5. To check the Project Details, i.e `project_structure`, `project_root`, `project_name`. 

       class ProjectData(SurroundData):

6. To check the Surround `files`, `Data`, `Directories`

       class Linter():
       linter_checks = Surround([CheckDirectories(), CheckFiles(), CheckData()])

### class Stage(ABC):

It replaces and Stores intermediate data from each stage in the pipeline to the Dump output of each stage.
             
    class Stage(ABC):
    def dump_output(self, surround_data, config):
    
**For Example:**
   
     from abc import ABC, abstractmethod
     class C(ABC):
     @abstractmethod
     def my_abstract_(cls, ...):
        ...
        
### class Frozen(): 

This class can toggle the ability of adding new attributes. 





