# Framework-Documentation-Part-II
#### This part is dedicated to explain the different **Classes** of Surround.
Classes run a means of bundling data and functionality together. Creating a new class creates a new type of object, allowing new instances of that type to be made. Each class instance can have attributes attached to it for maintaining its state. Class instances can also have methods defined by its class for modifying its state.

## Let us see some of the classes 

1.  class Config(Mapping):
2.  class LinterStage(Stage):
3.  class Stage(ABC):
4.  class Frozen(): 
5.  class SurroundData(Frozen):
6.  class Surround(ABC):
7.  class AllowedTypes(Enum):
8.  class Wrapper():

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

This class can toggle the ability of adding new attributes. `Frozen` classes are, then, classes which can't be changed after they've been created. 

In order to have a fully `frozen` class, all attributes of the class should hold immutable values too.

     """
    __isfrozen = False
    def __setattr__(self, key, value):
        if self.__isfrozen and not hasattr(self, key):
            raise TypeError("%r is a frozen object" % self)
        object.__setattr__(self, key, value)
        
### class SurroundData(Frozen):

Stores the data to be passed between each stage in Surround. Considering the frozen data as different stages inside the Surround are responsible for setting the attributes.

         """
        stage_metadata = []
        execution_time = None
        errors = []
        warnings = []
        
### class Surround(ABC):

The collections module has some concrete classes that derive from ABCs; these can be further derived. In addition, the collections.abc sub-module has some ABCs that can be used to test whether a class or instance gives a particular interface.

       def __init__(self, surround_stages=None, module=None):
         self.surround_stages = surround_stages

### class AllowedTypes(Enum):

An enum is a set of symbolic names or members bound to unique, constant values. Within an enumeration, the members can be compared by identity, and the enum itself can be repeated over and over.

       JSON = ["application/json"]
       FILE = ["file"]
       
### class Wrapper():






