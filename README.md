# MasterThesis-TestAutomationSystem

## Description
The repository contains source code of the Master Thesis  
"Oracle Cloud Infrastructure Compute Test Automation by distributing tests on multiple instances".

The system speeds up the time spent for automated testing by distributing the list of test scripts on  
multiple worker instances and running them simultaneously. It utilizes various technologies including  
Terraform, Ansible, Concourse, Docker, MEAN stack, and so on. A monitoring web application is provided  
to monitor test progress and also display test results. Evaluations show that the system reduces  
the execution time by 90 %.

Author: **Minh Gia Huy Cao**  
Matriculation number: 1148518  
M. Sc. High Integrity System  
Frankfurt University of Applied Sciences  
1st Supervisor: *Prof. Dr. Eicke Godehardt*  
2nd Supervisor: *Prof. Dr. Jörg Schäfer*

## Guideline
By default, when cloning a project with submodules, the directories containing submodules are cloned  
but have nothing inside. To clone the whole projects and its submodules, please use the command:

git clone --recurse-submodules https://github.com/CMGHuy/MasterThesis-TestAutomationSystem.git

In the future, after cloning the project, if there are any updates on the submodules, please run the following command to update:

git submodule update --remote

## Project structure
The following submodules support the clarification of the system:

1.  **Ansible**: *one of the three important parts of the system.*
    It contains all the Ansible playbook codes, which serve for different purposes including:
    - Provisioning essential software on the worker instances
    - Copying test configuration files (i.e. batchconfig.xml and mastersuite.csv) into the worker instances
    - Remote Desktop Control to the worker instances
    - Removing DISA resume file
    - Creating cron jobs for
        + Checking test progress continuously every 5 minute
        + Checking whether test execution has finished every 6 minute

2.  **AutomationScript**: *one of the three important parts of the system.*  
    It contains the bash script to automatize the whole system including the necessary commands  
    to execute Ansible, Terraform scripts, and other Java application, Python scripts.  
    This submodule is the controller of the whole system.

3.  **Terraform**: *one of the three important parts of the system.*  
    It contains the Terraform configuration files to create worker instances  
    with the desired configurations.

4.  **CheckTestProgress**: the Java application used to check test running progress.  
    The test progress is inserted into the monitoring web application and displayed on the web UI.

5.  **ConfigDownloader**: the Java application used to send the SOAP request to the Siebel application  
    to retrieve all Master suites description. Then, the batch configuration and master suite  
    of the desired Master suite are extracted.

6.  **Concourse-TestAutomation**: the Concourse pipeline configuration used to trigger automated testing
    without the need of logging into the master machine.

7.  **DatabaseInsertion**: the Java application used to insert test progress and test result  
    into the monitoring web application's database.

8.  **FileDivider**: the Java application used to divide the extracted master suite description  
    into multiple test sets based on the number of worker instances.

9.  **MonitoringWebApplication**: the full-stack monitoring web application used to monitor test progress  
    and display test results.

10.  **OpenTextAutomation**: the Java application used to interact with third-party application like OpenText.  
     Since Siebel Test Automation tool can not interact with external application, it needs to use this  
     application to handle complicated test cases.

11. **TemplateConverter**: the Java application used to convert the test report from worker instances back  
    to the original template.

12. **TestPlanner**: the Java application used to automatically change the Terraform configuration with respect to  
    the configuration specified in the automation script in submodule AutomationScript

In order to understand the flow, please read the AutomationScript submodule first.  
After that, please read the Ansible and Terraform code.  
For understanding how to use each Java application in the Ansible script,  
please find the corresponding submodule code to analyze.