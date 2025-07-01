## 309 Software Engineering Group - Hill Air Force Base

As a preface of this situation, much of the details of my work occurred in classified spaces. Accordingly, I must write with a level of obfuscation and generalization. Despite this, all of the information herein is accurately portrayed.

### Technical Program Manager (EDDGE/SABER): November 2022 - June 2023


### Machine Learning Research Fellow (DAF-MIT AI-Accelerator): November 2022 - June 2023




### F-16 Simulation Engineer (VOID): June 2021 - November 2022

The Viper OFP Integration and Development (VOID) simulator is a rapid feedback tool to support Operational Flight Program (OFP) development. There are four key components of the simulator: development builds of the OFP, simulated interfaces to external systems (such as physics or radios), an environment simulator for visualization, and several networked computers of different architectures and operating systems.

My efforts on this team focused on simulating external systems where I developed 3 new models and maintained several others. The general workflow for developing a new model involved consulting interface documentation, flight recordings, and subject matter experts to determine message flows for specified behaviors. Then emulating the proper 1553 message traffic in response to both environmental stimuli and message commands from the OFP. An interesting balance in this role involved finding the true operational behavior of a system to provide an accurate validation tool instead of simply trusting what the OFP expects.

I would like to highlight three things that make me proud from my time on this team. First was implementing unit testing. The VOID simulator is a mature project that has been in development for decades. Despite this, and the pressure to do so, no previous developer had successfully deployed a single unit test. I began writing unit tests using GoogleTest and integration tests for the new simulation models I developed. 

Second, I noticed that multiple simulation teams were duplicating significant amounts of effort be developing the same simulation models independently. 

