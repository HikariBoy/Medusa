### Medusa - An Educational tool to support Engineering/Science based assessment and feedback via the Blackboard Learning Management System
Here you will find the release versions of <b>Medusa (an adult jellyfish)</b>, a tool developed at [The University of Western Australia](https://research-repository.uwa.edu.au/en/persons/adrian-keating) (UWA),
## Installation
> NOTE: the 70 Mbyte EXE file is currently hosted on github's Large File Storage (LFS) which does not alllows the EXE to be downloaded (so the file cannot be downloaded from here).  If you wnat a copy of the EXE to try out, get in contact with me.

Once downloaded, extract the zip file and a Medusa-master folder will be created.  Change into this folder and start the Medusa.exe program.  Once Medusa starts select <b>[HELP]</b> and follow the Quick-Start Guide to see it in action.  Example Answer and Results files are provided to explore how Medusa works.  

>It is essential that the <b>FeedbackReport.html</b> and the <b>Help Folder</b> are locatd in the same directory as the <b>Medusa.exe</b> program.  

## Overview
Medusa provides a method to automate grading of detailed, multi-part questions used in the BlackBoard Learning Management System.  Detailed, multi-part questions (which have for example Parts [a] to [f]) are interconnected questions which demonstrate the ability to solve a larger (real-world) problem,
taking onboard all the information provided.  Such question styles are requires, especially towards the end of a unit, in order for
students apply, analyse, synthesize and evaluate [(Levels 3-6 of Bloom’s Taxonomy)](https://learningcenter.unc.edu/tips-and-tools/higher-order-thinking/)
information through processes they have learnt throughout the unit.  Typical Blakcboard (and indead most LMS systems) only ask isolated,
short answer type quesitons - as soon as randomisation of a question bank is used in order to reduce instances of collusion, it is no
longer posible to create interconnections between the different short answer questions offered in Blackboard (the randomisation breaks any links).  
Medusa can grade detailed, multi-part Blackboard questions after they have been deployed on Blackboard, answered by students and the
 results [downloaded via the grade center](https://utlv.screenstepslive.com/s/faculty/m/BlackboardLearn/l/186048-downloading-test-and-survey-results).  This system _assumes_ you are interested in building detailed, multi-part Blackboard questions using
 [Blackboard](https://help.blackboard.com/Learn/Instructor/Tests_Pools_Surveys/Question_Types/Fill_in_Multiple_Blanks_Questions), a process which I have
 previously discussed with my own [insights](https://github.com/HikariBoy/BlackBoard-Multipart-Questions).  However Medusa will also work on standards Blackboard questions such as multiple-choice and fill in the blank. Medusa and Multi-part Blackboard style questions were trialed during an examination of 221 students in a unit Mid-sem exam at UWA in April 2020.   
## Issues with Blackboard
  Key problems with grading using LMS specifically for <b>engineering/science units</b> (which generally require units and application of algorithmic methods to a problem) are:
 * Blackboard does not allow for a range of student inputs.  For example, answers of 0.002A, 2mA, 2X10^-3A, 2e-3A and even 2e-6kA should all be marked as correct for an answer of 2mA.  Experience shows that students can use such expressions, sometimes simply to try to break the system.  Blackboard does allow for [regular expressions](https://www.regular-expressions.info/tutorial.html) which can pattern match to these and [I have written about these features](https://github.com/HikariBoy/BlackBoard-Multipart-Questions), however significant effort is required for every instance of an input to catch such entries.  Such effort is largely a waste of time for the unit-coordinator and graders as the effort needs to be repeated (and tested) for every new question.
* Blackboard does not take into account follow-on (carry-forward) mistakes by the student.  Where a mistake is made early in a multi-part
([multiple fill in the blank](https://help.blackboard.com/Learn/Instructor/Tests_Pools_Surveys/Question_Types/Fill_in_Multiple_Blanks_Questions)) the entire
problem is marked as wrong.
* As a result of the 2nd point, Blackboard largely encourages the use of single, short answer type questions.  However such
questions cannot be connected together when they are added to a question pool and then selected at random, an essential element to minimise collusion
in on-line, non-invigilated (non-proctored) tests.
* Blackboard does not provide personalised feedback to the students.  Where a random pool is used, only a generic answer method can be provided to the student.
* Blackboard questions cannot be checked for collusion easily


## The proposed solution -Medusa
Medusa was developed specifically adresses these points above to enable a better assessment and more detailed, personallised feedback
to each stduent to help their learning.  The program automatically generates an assessment and commented feedback pdf document, containing
personalised statistics for each student.  Just as importantly to ensure the integrity of the test, the code checks for possible collusion and flags
 any papers that need to be checked more throughly by the unit-coordinator.  This can be considered <b>post-invigilation (post-proctoring)</b> and is
 perhaps a more realistic method of ensuring text integrity than having someone present to watch over as the test is taken.  

### Features of the grading program  are:

* Data input is accepted with a range of SI units (A, Amps or Amperes) and a range of prefixes (mA,kV).  Units can be combined using /,.,* and ^ operators to form units such as m/s, m.N or kg.m/s^2.  Prefex can be used but only for the first unit, so for example mm.N  (millimetre times newton) would be accepted as an answer from a student but mm.mN (millimetre times millinewton) will not.  Medusa does it’s best to flags issues with content it cannot interpret and moves such files into a ./GradingIssues directory for checking but the unit coordinator.  
* The answer file specifies the method to solve. Follow-through (carry-forward) marks are awarded if the student applies the correct method. Solutions are checked for the accepted answer as well as the answer based on a correct method applied to previously wrong answers. The feedback provided to students tells them the answer was wrong but such consideration was taken into account and correct marks awared where appropriate. This feature can be turned off but it is discouraged to do that.  
* To aid answer file creating, the option to build an answer file or the test completed based on the most common values and units input by students is provided by Medusa.
* The answer file specifies the method to solve. Follow-through (carry-forward) marks are awarded if the student applies the correct method. Solutions are checked for the accepted answer as well as the answer based on a correct method applied to previously wrong answers. The feedback provided to students tells them the answer was wrong but such consideration was taken into account and correct marks awared where appropriate. This feature can be turned off but it is discouraged to do that.
* Feedback is provided if students are out by factors of 10,100, 1000.  
* Feedback is provided where units are wrong or missing and marks awarded accordingly.  
* For number based answers, the magnitude, sign and units are all checked and can each be assigned marks separately.  
* The letter o and O when found before other numbers are considered to be typos and converted to ZERO (0).  
* Numbers are accepted in a variety of formats. A value of 0.0123A can be accepted as 12.2mA, 12.3e-3A, 12.3x10^-3A and even 12.3e-9MA.  
* Different rubrics can be assigned to different questions. Number based problems and word/sentence based answers have separate rubrics when grading.  
* Each part of every question can be assigned a different weight  
* A pdf is generated for each student with detailed feedback for each part of the question  
* A personalized histogram is created or each student, along with statistics for the unit (perhaps the best way to have students learn statistics is to provide such imformation)  
* Will grade N questions from a question-bank (pool) of M questions where N<=M (for example a question bank may have M=10 questions of which students are randomly assigned N=5)  
* Text based answers can have multiple answers including a regular expression, for example you can input any number of text basd answers such as "KCL" and "Kirchhoff’s Current Law" and/or include a regular expression such as "Kirch([h])?of([f])?[\W]?[s]? Curr[ea]nt Law[s]. All these forms would all be accepted as correct for answer requiring identification of Kirchhoff’s Current Law. For more information on forming and testing regular expressions, see here.  
* Runs a collusion check against all student answers. Specifcially, it checks for any student that answers questions that they were not assigned, for example, where a student gets a question largely correct however it was not one of the questions from the random question bank (pool) they were assigned. This suggest the student may have sat next to someone and simply copied their answers into their text entry fields. Such instances are flagged to the unit-coordinator to investigate and possibly interview the students involved. answers a question  


><b>Disclaimer </b>- This is an open source project and no claims are made about the accuracy or validity of the code including, but not limited to, performing grading and giving feedback. The code is not to be used for purposes for which it was not designed without the express permission of the author. Unit coordinators should in all cases check the ouput provided and consider possible errors that might arise either from the code it's self or from the files that it inputs. Students should be allowed to review and comment on the grade produced.
