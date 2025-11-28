# Imperatives & Should — PRS System 
Our project SIGEI, a system designed to modernize the educational management of public preschool institutions that serve children aged 3 to 5. From the beginning, we aimed to create a platform that truly supports principals, teachers, and administrative staff, so we had to analyze, organize, and transform the processes that are still handled manually. SIGEI not only centralizes academic and administrative information; it also allows users to visualize, control, and optimize daily tasks within each institution.

The system has been built with a horizontally scalable architecture, enabling it to grow, adapt, and operate across multiple schools without losing performance. In addition, SIGEI should provide clear, accessible, and real-time information so that school staff should be able to make informed decisions, should manage enrollment, attendance, and student progress easily, and should improve institutional coordination from a single dashboard.

During the development of this project, we set out to explain, demonstrate, and document every technical step using tools such as Python, ETL processes, Pandas, and Looker Studio, ensuring that the system meets, functions, and adapts to the real needs of the educational environment. With SIGEI, we aim to deliver a reliable, intuitive, and efficient platform that contributes to a more organized and modern early-education system.

## 1. Student and Tutor Management

### **Imperatives**
- Register the student with accurate personal data.  
- Verify the tutor’s identity prior to account creation.  
- Complete the tutor-student linkage in the system.  

### **Should (Advisory)**
- You should ensure that every student is registered using validated and complete personal information to maintain administrative accuracy and legal compliance.  
- You should verify tutors’ identities (document checks and contact confirmation) before provisioning access, in order to protect minors and preserve institutional integrity.  
- You should link tutors and students in the database consistently, maintaining referential integrity and enabling reliable communication channels.  


---

## 2. Classroom and Institution Management

### **Imperatives**
- Assign each child to the appropriate classroom.  
- Update classroom capacities immediately after enrollment changes.  
- Confirm each institution’s operational status before admitting students.  

### **Should (Advisory)**
- You should assign children to classrooms according to age-group and pedagogical criteria (3, 4, 5 years) to support curriculum alignment and safety.  
- You should update capacity records without delay to avoid over-enrollment and to support resource planning.  
- You should verify the institution’s accreditation and operational status prior to enrollment to prevent administrative inconsistencies and legal issues.  


---

## 3. Enrollments (Matrículas)

### **Imperatives**
- Process the enrollment transaction atomically.  
- Validate required documentation before finalizing enrollment.  
- Notify tutor and institution upon successful matrícula.  

### **Should (Advisory)**
- You should implement enrollment as an atomic operation (or a clear compensating transaction) so that partial states are avoided and data consistency is preserved across related entities (student, tutor, classroom, institution).  
- You should validate all mandatory documents (identity, consent, health records where required) prior to committing the matrícula to ensure compliance with institutional and regulatory standards.  
- You should notify the tutor, classroom teacher, and institutional administrator automatically after enrollment to guarantee timely pedagogical preparation and operational coordination.  


---

## 4. Notes and Academic Records

### **Imperatives**
- Record assessment results accurately and promptly.  
- Apply standardized evaluation criteria consistently.  
- Restrict grade editing to authorized personnel.  

### **Should (Advisory)**
- You should record students’ assessment results in a timely manner using the defined data model to prevent inconsistencies and preserve academic history.  
- You should apply standardized evaluation rubrics across classrooms to enable comparable assessment and meaningful reporting.  
- You should restrict editing of academic records to designated roles (e.g., authorized teachers or administrators) and log all modifications for auditability.  


---

## 5. System Security and Data Protection

### **Imperatives**
- Do not expose personally identifiable information.  
- Enforce role-based access control for administrative functions.  
- Use secure channels for all external integrations.  

### **Should (Advisory)**
- You should encrypt personally identifiable information both in transit and at rest, following national and sector-specific privacy requirements for minors.  
- You should implement role-based access control (RBAC) so that directors, tutors, and administrative staff have only the permissions required to perform their duties.  
- You should secure all integrations (APIs, third-party services) with TLS and appropriate authentication to protect the integrity and confidentiality of data exchanges.  


---

## 6. System Operation, Observability and Resilience

### **Imperatives**
- Monitor service health and performance continuously.  
- Scale enrollment processing horizontally under load.  
- Log and retain significant events and errors.  

### **Should (Advisory)**
- You should deploy monitoring and alerting (metrics, traces, logs) to detect performance degradations and failures promptly, enabling proactive operational responses.  
- You should enable horizontal scaling for the enrollment service so that it can absorb traffic spikes (e.g., mass matriculation periods) while maintaining service-level objectives.  
- You should implement structured logging and retain audit trails for key events (enrollments, grade changes, administrative actions) to support troubleshooting and compliance reviews.  


---

## 7. Integration and Data Consistency

### **Imperatives**
- Publish enrollment events to the integration bus.  
- Reconcile cross-service records periodically.  
- Retry transient integration failures automatically.  

### **Should (Advisory)**
- You should emit well-defined domain events (e.g., `EnrollmentCreated`, `EnrollmentCancelled`) to an asynchronous broker to ensure eventual consistency and decoupled integrations.  
- You should schedule periodic reconciliation jobs to detect and correct inconsistencies between microservices (students, enrollments, classrooms, institutions).  
- You should implement idempotent operations and exponential backoff retries for transient failures to improve robustness of inter-service communications.  
