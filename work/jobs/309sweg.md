## 309 Software Engineering Group - Hill Air Force Base

As a preface of this situation, much of the details of my work occurred in classified spaces. Accordingly, I must write with a level of obfuscation and generalization. Despite this, all of the information herein is accurately portrayed.

### Technical Program Manager (EDDGE/SABER): June 2023 - June 2025


### Machine Learning Research Fellow (DAF-MIT AI-Accelerator): November 2022 - May 2023

The Department of the Air Force (DAF) has partnered with MIT to accelerate the development and fielding of key artificial intelligence (AI) capabilities in a partnership called the [DAF-MIT AI Accelerator](https://www.aiaccelerator.af.mil/) (AIA). As part of this program, the Air Force cycles airmen through a 5-month fellowship, called the [Phantom Fellowship](https://www.aiaccelerator.af.mil/Phantom-Program/), to spread cutting edge AI knowledge throughout the force. I was selected for this highly competitive program in a cohort of 12 other Phantoms.

Half of my assignment during the Phantom Fellowship was working with MIT and Lincoln Lab researchers. I was assigned to the Responsible AI team that researched robustness and explainability topics in partnership with the [Responsible AI](https://www.ll.mit.edu/r-d/projects/responsible-ai-toolbox) team and [Dr. Aleksander Mądry](https://madry.mit.edu/). My specific tasks explored improving the robustness of a model to domain shift using an adversarial training regimen. 

In addition to the work with the Responsible AI team, I produced a novel research paper on machine learning applications at the maintenance repair depot at Hill Air Force Base. I identified several promising opportunities for improving existing workflows with AI/ML by interviewing a wide swath of practitioners and subject matter experts. My findings were received with high praise and presented to several high leaders back at Hill AFB. After my time at the AIA concluded, I was asked to condense my report to a 2-page extended abstract for submission to [HPEC 2023](https://ieee-hpec.org/index.php/ieee-hpec-2023-prelim-agenda/). This is my first publication to an academic conference, which I am quite proud of. Many details were distilled and removed to prepare the document for public release, but I'm happy to be able to share it here:

<object data="HPEC2023_paper.pdf" type="application/pdf" width="700px" height="700px">
    <embed src="AbstractMlApplicationsAtHill.pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="AbstractMlApplicationsAtHill.pdf">Download PDF</a>.</p>
    </embed>
</object>

I was awarded with the Director's Impact Award at the end of this fellowship. This award is given to the highest performing Phantom in each cohort as determined by both peers and leadership. The cohort unanimously voted me for this role because I quickly became the group's "go-to" expert for peer technical support and advice. I additionally extended my impact by participating in, and by many metrics "winning", the [Bravo 10 Hackathon](https://www.dafcio.af.mil/News/Article-Display/Article/3443413/air-force-special-operations-command-hosts-us-air-force-multi-classification-ha/) where I developed and implemented the key novelty on Team Yodacorn and was awarded with "Best Use of AI/ML" and "Most Inventive". I also was selected to participate in a public affairs event where we conducted an ["AMA"](https://www.reddit.com/r/AirForce/comments/10kbitk/im_dr_ethan_sneider_program_manager_for_the/) on Reddit. This high level of performance in my expected role, and expansion beyond expectations led leadership to select me for the Director's Impact Award honor.

After the fellowship I had the pleasure of being featured in three news articles. The first was published by [Hill Air Force Base Public Affairs](https://www.reddit.com/r/AirForce/comments/10kbitk/im_dr_ethan_sneider_program_manager_for_the/) to highlight my experience. During that process, a reporter with KSL contacted the same public affairs office asking for an interview on artificial intelligence in defense in response to a rise in interest on the topic due to the recent release of ChatGPT. I got to [interview with the KSL](https://www.ksl.com/article/50599231/heres-how-hill-air-force-base-is-navigating-the-rapid-rise-of-artificial-intelligence) reporter and discuss my thoughts on the AI field at large. Finally, the AIA itself released a statement on my capstone project being [published](https://aia.mit.edu/2023/08/31/daf-mit-ai-accelerator-research-projects-featured-at-ieee-hpec-conference/) to HPEC 2023.



### F-16 Simulation Engineer (VOID): June 2021 - November 2022

The Viper OFP Integration and Development (VOID) simulator is a rapid feedback tool to support Operational Flight Program (OFP) development. There are four key components of the simulator: development builds of the OFP, simulated interfaces to external systems (such as physics or radios), an environment simulator for visualization, and several networked computers of different architectures and operating systems.

My efforts on this team focused on simulating external systems where I developed 3 new models and maintained several others. The general workflow for developing a new model involved consulting interface documentation, flight recordings, and subject matter experts to determine message flows for specified behaviors. Then emulating the proper 1553 message traffic in response to both environmental stimuli and message commands from the OFP. An interesting balance in this role involved finding the true operational behavior of a system to provide an accurate validation tool instead of simply trusting what the OFP expects.

I would like to highlight three things that make me proud from my time on this team. First was implementing unit testing. The VOID simulator is a mature project that has been in development for decades. Despite this, and the pressure to do so, no previous developer had successfully deployed a single unit test. I began writing unit tests using GoogleTest and integration tests for the new simulation models I developed. 

Second, I noticed that multiple simulation teams were duplicating significant amounts of effort be developing the same simulation models independently. Seeing this problem and the opportunity for inter-team collaboration, I led an effort to create an implementation agnostic framework to make core simulation modules valuable for any team. In this framework, I standardized an interface that abstracted simulator specific behaviors, such as 1553 traffic, pilot vehicle interface (PVI) or external physical stimuli.

A final highlight in this time was to improve several modules in the VOID simulation core. The core simulator ran on multiple low resource compute boards running a real time operating system (RTOS) that were of similar architecture to the aircraft Line Replaceable Units (LRUs). These boards were overloaded with all simulation activity and were beginning to perform poorly, when only the OFP code needed to be run on them. I developed a tool to synchronize the mux state between multiple machines using Redis such that a majority of the simulation modules could be offloaded from the boards. I validated this tool using a suite of stress tests and used it in two external models.

