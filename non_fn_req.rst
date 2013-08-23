Other non-functional requirements
=================================

	**Performance requirements**

		Since it is an online platform, hence the delay involved in system interaction must be less else the user will feel that the 			system is down. In case of JavaScript interactions the delay involved is less than 3 seconds. The sorting and searching of 			course takes place in less than 1 second.

	**Safety and Security Requirements**

		The form submissions are validated by csrf tokens, hence protecting it from spammers. User authentication is done by 			encrypting the session login variable. Users are required to confirm their identity by responding to a confirmation mail. Each 			service integration is protected by secret key. Thus, there is no possibility of intrusion. 


	**Software quality attributes**

		- Availability

			Availability means more than just being up and running 24/7/365, availability also means that the web software must be 				available when accessed by diverse browsers. Hence, the application must be accessible in its original form across 				multiple browsers of all platforms.

		- Reliability
			
			If web software is unreliable, websites that depend on the software will lose users. Grading of students is crucial 				data and the software must be reliable to keep them intact. User submissions are like transactions as they affect the 				grades of the students, hence it should have quality testing measures.

		- Scalability
			
			The system should be highly scalable and modular in design to alter features as required





