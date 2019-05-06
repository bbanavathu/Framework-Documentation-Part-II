# Framework-Documentation-Part-II
#### This part is dedicated to explain the different **Classes** of Surround.
Classes run a means of bundling data and functionality together. Creating a new class creates a new type of object, allowing new instances of that type to be made. Each class instance can have attributes attached to it for maintaining its state. Class instances can also have methods defined by its class for modifying its state.

### Let us see some of the classes 
1. 	class Frozen():
2.	class SurroundData(Frozen):
3.	class Surround(ABC):
4.	class AllowedTypes(Enum):
5.	class Wrapper():
6.	class Stage(ABC):
7.	class LinterStage(Stage):
8.	class CheckData(LinterStage):
9.	class CheckFiles(LinterStage):
10.	class CheckDirectories(LinterStage):
11.	class ProjectData(SurroundData):
12.	class Linter():
13.	class Config(Mapping):
14.	class HelloStage(Stage):
15.	class BasicData(SurroundData):
16.	class TestSurround(unittest.TestCase):
17.	class TestConfig(unittest.TestCase):

### Class Config(Mapping): 

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
            
### Class LinterStage(Stage):

This class helps in verifying the quality of the code and analyse source code for potential erros,
lint is a tool which is used to mark the source code with some suspicious and non-structural.

**These Classes Add support for the RUnning Project specific tasks**













