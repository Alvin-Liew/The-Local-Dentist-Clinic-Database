# The-Local-Dentist-Clinic-Database

## Project Milestone #1 Proposal

### Business Scenario:
Our company has ran a local dentist clinic in downtown Brooklyn. We have been keeping our records of patients, appointments, and payments using spreadsheets and log sheets. We would like to transition to a more efficient way of collecting data using a database.

In our business, we have different types of dental and orthodontic procedures such as teeth cleaning, fillings, restorations, tooth extractions, root canals, dentures, retainers, metal braces, gums care, etc. We need to keep track of materials (Dental equipment) used in the procedures. While each service has a standard price, insurance may affect the actual amount due to the patient. 

We also need to keep track of each patient’s contact information as well as their insurance providers and dental history. We need to keep track of our employees including their home addresses, contact information, and pay rates. For appointments, we need to know the date and time of appointments and which patient the appointment is for.

### List of Entities/Attributes:
Appointment - Appointment_ID, appointment_time, appointment_date, Examination_Room
Patient - Patient_ID, Firstname, Lastname, street, city, state, zipcode, Phonenumber, Emailaddress, insurance, dental_history
Payment - 
Dental service - Dental service_ID, service_name, service_price, service_equipment
Employee/Provider - Employee_ID, Firstname, Lastname, street, city, state, zip code, Phonenumber, EmailAddress, Employee_Role, Paytype, PayRate, and PayTimePeriod
SpecificServiceRendered- SpecificServiceRendered_ID, Cost, Insurance_Coverage, Amount_Due

## Project Milestone #2 Systems Analysis and E-R Model

### E-R Diagram

![image](https://github.com/Alvin-Liew/The-Local-Dentist-Clinic-Database/assets/105011531/e9a5f171-6467-47bb-8879-9a4da8e24bc1)

### Relationship Sentences:
One Payment History must be made by one and only one Patient 
One Patient may be making one or more Payment History
One Patient may be making one or more Appointment(s)
One Appointment must be a time set aside for one and only one Patient
One Appointment may be reserving one or more SpecificServiceRendered
One SpecificServiceRendered must be rendered during one and only one Appointment
One SpecificServiceRendered must be a rendering of one and only one Dental Service
One Dental Service may be rendered as one or more SpecificServiceRendered
One SpecificServiceRendered must be rendered by one and only one Employee
One Employee may be rendering one or more SpecificServiceRendered

##Project Milestone #3 Logical and Physical Modeling 

### Relational Model:
Appointment (Appointment_ID(Key), Appointment_Time, Appointment_Date, Examination_Room,Patient_ID(FK))
Patient (Patient_ID(Key), Firstname, Lastname, Street, City, State, Zipcode, Phonenumber, EmailAddress, Insurance, Dental_History)
SpecificServiceRendered (SpecificServiceRendered_ID(Key), Cost, Insurance_Coverage, Amount_ Due, Appointment_ID(FK), Employee_ID(FK), Dental_Service_ID(FK))
Dental Service (Dental_Service_ID(Key), Service_Name, Service_Price
Service_Equipment)
Employee(Employee_ID(Key), Firstname, Lastname, Street, City, State, Zipcode, Phonenumber, EmailAddress, Employee_Role, Paytype, PayTimePeriod)
Payment History(Payment_ID(Key), Payment_Date, Payment_Method, Payment_Amount, Patient_ID(FK))

### Functional Dependencies:

Appointment (Appointment_ID(Key), Appointment_Time, Appointment_Date, Examination_Room,Patient_ID(FK))
 FD1: Appointment_ID -> Appointment_Time, Appointment_Date, Examination_Room, Patient_ID(fk)

1NF: Yes, because it meets the definition of a relation
2NF: Yes, because all the non-keys are dependent on all the keys, no partial key dependencies 
3NF: Yes, there are no transitive dependencies

Patient (Patient_ID(Key), Firstname, Lastname, Street, City, State, Zipcode, Phonenumber, EmailAddress, Insurance, Dental_History)

  FD1: Patient_ID-> Firstname, Lastname, Street, City, State, Zipcode, Phonenumber, EmailAddress, Insurance, Dental_History 

  FD2: Zipcode-> City, State

1NF: Yes, because it meets the definition of a relation
2NF: Yes, because all the non-keys are dependent on all the keys, no partial key dependencies 
3NF: No, there are transitive dependices: PatientID-> Zipcode and Zipcode-> City, State, therefore PatientID ->City, State.  We need to split Patient into two new relations 

### NORMALIZATION:

Zipcodes(Zipcode(key), City, State)
FD1:Zipcode-> City, State

1NF: Yes, because it is split from a relation
2NF: Yes, because all the non-keys are dependent on all the keys, no partial key dependencies 
3NF: Yes, there are no transitive dependencies

Patient_1 (Patient_ID(Key), Firstname, Lastname, Street, Zipcode, Phonenumber, EmailAddress, Insurance, Dental_History)
	FD1: Patient_ID-> Firstname, Lastname, Street, Zipcode, Phonenumber, 
EmailAddress, Insurance, Dental_History 
1NF: Yes, because it is split from a relation
2NF: Yes, because all the non-keys are dependent on all the keys, no partial key dependencies 
3NF: Yes, there are no transitive dependencies

### DE-NORMALIZATION 

We need to return the relation Patient to its original form. 

Patient (Patient_ID(Key), Firstname, Lastname, Street, City, State, Zipcode, Phonenumber, EmailAddress, Insurance, Dental_History)


SpecificServiceRendered (SpecificServiceRendered_ID, Cost, Insurance_Coverage, Amount_ Due, Appointment_ID(FK), Employee_ID(FK), Dental_Service_ID(FK))
	FD1: SpecificServiceRendered_ID -> Cost, Insurance_Coverage, Amount_ Due, 	Appointment_ID(FK), Employee_ID(FK), Dental_Service_ID(FK)

1NF: Yes, because it meets the definition of a relation
2NF: Yes, because all the non-keys are dependent on all the keys, no partial key dependencies 
3NF: Yes, there are no transitive dependencies


Dental Service (Dental_Service_ID(Key), Service_Name, Service_Price
Service_Equipment)
	FD1: Dental_Service_ID-> Service_Name, Service_Price
Service_Equipment

1NF: Yes, because it meets the definition of a relation
2NF: Yes, because all the non-keys are dependent on all the keys, no partial key dependencies 
3NF: Yes, there are no transitive dependencies


Employee(Employee_ID(Key), Firstname, Lastname, Street, City, State, Zipcode, Phonenumber, EmailAddress, Employee_Role, Paytype, PayTimePeriod)
	FD1: Employee_ID->Firstname, Lastname, Street, City, State, Zipcode, Phonenumber, EmailAddress, Employee_Role, Paytype, PayTimePeriod
	FD2: Zipcode-> City, State 

1NF: Yes, because it meets the definition of a relation
2NF: Yes, because all the non-keys are dependent on all the keys, no partial key dependencies 
3NF: No there are transitive dependencies: Employee_ID-> Zipcode and Zipcode-> City, State, therefore Employee_ID->City, State.. We need to split Employee into two new relations 

### NORMALIZATION

Zipcodes(Zipcode(key), City, State)
FD1:Zipcode-> City, State

1NF: Yes, because it is split from a relation
2NF: Yes, because all the non-keys are dependent on all the keys, no partial key dependencies 
3NF: Yes, there are no transitive dependencies

Employee_1(Employee_ID(Key), Firstname, Lastname, Street, Zipcode, Phonenumber, EmailAddress, Employee_Role, Paytype, PayTimePeriod)

FD1: Employee_ID->Firstname, Lastname, Street, Zipcode, Phonenumber, EmailAddress, Employee_Role, Paytype, PayTimePeriod

1NF: Yes, because it is split from a relation 
2NF: Yes, because all the non-keys are dependent on all the keys, no partial key dependencies 
3NF: Yes, there are no transitive dependencies

## Project Milestone #4 Database Implementation

### Creating Tables:

Appointment (Appointment_ID(Key), Appointment_Time, Appointment_Date, Examination_Room,Patient_ID(FK))

CREATE TABLE Appointment
(
	Appointment_ID		VARCHAR(10) NOT NULL,
	Appointment_DateTime	DATE,
	Examination_room		VARCHAR(2),
Patient_ID			VARCHAR(10) NOT NULL,	
	PRIMARY KEY (Appointment_ID)
)

Patient(Patient_ID(Key), Firstname, Lastname, Street, Zipcode, City, State, Phonenumber, EmailAddress, Insurance, Dental_History)

CREATE TABLE Patient
(
	Patient_ID	   VARCHAR(10) NOT NULL,
	Firstname	   VARCHAR(35),
	Lastname	   VARCHAR(25),
	Street		   VARCHAR(35),
	Zipcode	  VARCHAR(12),
	City     	  VARCHAR(36), 
State      	  VARCHAR(2),
	Phonenumber  VARCHAR(15),
	EmailAddress   VARCHAR(255),
	Insurance	   VARCHAR(255),
	Dental_History   Date,
	PRIMARY KEY (Patient_ID)
)

SpecificServiceRendered (SpecificServiceRendered_ID, Cost, Insurance_Coverage, Amount_ Due, Appointment_ID(FK), Employee_ID(FK), Dental_Service_ID(FK))

CREATE TABLE SpecificServiceRendered
(
	SpecificServiceRendered_ID	VARCHAR(10) NOT NULL,
Cost					NUMBER, 
Insurance_Coverage		NUMBER, 
Amount_Due				NUMBER,
Appointment_ID 			VARCHAR(10) NOT NULL,
 	Employee_ID			VARCHAR(10) NOT NULL,
	Dental_Service_ID			VARCHAR(10) NOT NULL,
PRIMARY KEY (SpecificServiceRendered_ID)
)


DentalService (Dental_Service_ID(Key), Service_Name, Service_Price
Service_Equipment)

CREATE TABLE DentalService
(
	Dental_Service_ID	VARCHAR(10) NOT NULL, 
Service_Name 	VARCHAR(35),
Service_Price	NUMBER,
Service_Equipment VARCHAR(255),
PRIMARY KEY (Dental_Service_ID)
)

Employee(Employee_ID(Key), Firstname, Lastname, Street, Zipcode, City, State, Phonenumber, EmailAddress, Employee_Role, Paytype, PayTimePeriod)

CREATE TABLE Employee
(
	Employee_ID	VARCHAR(10) NOT NULL, 
Firstname		VARCHAR(35), 
Lastname		VARCHAR(25), 
Street			VARCHAR(45), 
Zipcode	  	VARCHAR(12),
City     	  	VARCHAR(36), 
State      	  	VARCHAR(2),
Phonenumber	VARCHAR(15), 
EmailAddress	VARCHAR(225), 
Employee_Role	VARCHAR(225), 
Paytype		VARCHAR(6), 
PayTimePeriod	VARCHAR(11),
	PRIMARY KEY (Employee_ID)
)

PaymentHistory(Payment_ID(Key), Payment_Date, Payment_Method, Payment_Amount, Patient_ID(FK))

CREATE TABLE PaymentHistory
(
Payment_ID		VARCHAR(10) NOT NULL, 
Payment_Date	DATE, 
Payment_Method	VARCHAR(20), 
Payment_Amount	NUMBER,
Patient_ID		VARCHAR(10) NOT NULL, 
PRIMARY KEY (Payment_ID)
)

### Adding Foreign Keys:

ALTER TABLE Appoinment
	ADD CONSTRAINT fk_patient_appointment		
FOREIGN KEY (Patient_ID)
			REFERENCES Patient (Patient_ID)

ALTER TABLE SpecificServiceRendered
	ADD CONSTRAINT fk_ServiceRendered_Appointment
		FOREIGN KEY (Appointment_ID)
			REFERENCES Appointment (Appointment_ID)

ALTER TABLE SpecificServiceRendered
	ADD CONSTRAINT fk_ServiceRendered_Employee
		FOREIGN KEY (Employee_ID)
			REFERENCES Employee (Employee_ID)

ALTER TABLE SpecificServiceRendered
	ADD CONSTRAINT fk_ServiceRendered_DentalService
		FOREIGN KEY (Dental_Service_ID)
			REFERENCES DentalService (Dental_Service_ID)

ALTER TABLE PaymentHistory
	ADD CONSTRAINT fk_patient_paymenthistory
		FOREIGN KEY (Patient_ID)
			REFERENCES Patient (Patient_ID)

### Adding Data to the Tables:

INSERT INTO Appointment VALUES ('A600’, ‘11/18/2022 10:30:00 AM’, ‘E01’, ‘P101’);
INSERT INTO Appointment VALUES ('A601’, ‘11/20/2022 04:00:00 PM’, ‘E02’, ‘P102’);
INSERT INTO Appointment VALUES ('A602’, ‘11/20/2022 06:30:00 PM’, ‘E03’, ‘P103’);
INSERT INTO Appointment VALUES ('A603’, ‘11/30/2022 11:00:00 AM’, ‘E04’, ‘P104’);
INSERT INTO Appointment VALUES ('A604’, ‘12/14/2022 02:00:00 PM’, ‘E05’, ‘P105’);
INSERT INTO Appointment VALUES ('A605’, ‘12/22/2022 09:00:00 AM’, ‘E06’, ‘P106’);
INSERT INTO Appointment VALUES ('A606’, ‘01/04/2023 01:30:00 PM’, ‘E07’, ‘P107’);
INSERT INTO Appointment VALUES ('A607’, ‘01/27/2023 05:30:00 PM’, ‘E08’, ‘P108’);

INSERT INTO Patient VALUES ('P101’, ‘Kirk’, ‘Meadows’, ‘70-26 Fleet St’, ‘11375’, ‘Queens’, ‘NY’, ‘518-579-2601’, ‘kirkmeadows03@gmail.com’, ‘CIGNA’, ‘11/18/2021 10:30:00 AM’);
INSERT INTO Patient VALUES ('P102’, ‘Zion’, ‘Byrne’, ‘104-32 43 Avenue’, ‘11368’, ‘Queens’, ‘NY’, ‘718-923-8014’, ‘zionbyrne11368@gmail.com’, ‘United Concordia Cos. Inc.’, ‘11/20/2022 04:00:00 PM’);
INSERT INTO Patient VALUES ('P103’, ‘Sumayya’, ‘Lindsey’, ‘1436 51st ST’, ‘11219’, ‘Brooklyn’, NY’, ‘607-274-2388’, ‘sumayyalindsey234@gmail.com’, ‘WellPoint Inc.’, ‘11/20/2022 06:30:00 PM’);
INSERT INTO Patient VALUES ('P104’, ‘Bernadette’, ‘Vargas’, ‘138 Midwood St’, ‘11225’, ‘Brooklyn’, NY’, ‘516-728-7202’, ‘bernadettevargas101@gmail.com’, ‘Ameritas Group Dental’, ‘11/30/2022 11:00:00 AM’);
INSERT INTO Patient VALUES ('P105’, ‘Mahdi’, ‘Sweet’, ‘173 Waverly Pl’, ‘10014’, ‘Manhattan’, NY’, ‘347-345-4114’, ‘mahdisweet207@outlook.com’, ‘Aetna Inc.’, ‘12/14/2021 02:00:00 PM’);
INSERT INTO Patient VALUES ('P106’, ‘Shaan’, ‘Lindsay’, ‘51 Studio Ln’, ‘10304’, ‘Staten Island’, NY’, ‘347-320-0914’, ‘shaanlindsay42@outlook.com’, ‘CIGNA’, ‘12/22/2022 09:00:00 AM’);
INSERT INTO Patient VALUES ('P107’, ‘Mustafa’, ‘Busby’, ‘2118 Bay Ridge Pkwy’, ‘11204’, ‘Brooklyn’, NY’, ‘914-213-5833’, ‘mustafabusby02@gmail.com’, ‘MetLife Inc.’, ‘01/04/2023 01:30:00 PM’);
INSERT INTO Patient VALUES ('P108’, ‘Arwel’, ‘Hogan’, ‘133 E 66th St’, ‘10065’, ‘Manhattan’, NY’, ‘646-662-9574’, ‘arwelhogan567@gmail.com’, ‘Aetna Inc.’, ‘01/27/2023 05:30:00 PM’);

INSERT INTO SpecificServiceRendered VALUES ('SSR101’, ‘200’, ‘200’, ‘0’, 'A600’, 'E001’, 'DS03’);
INSERT INTO SpecificServiceRendered VALUES ('SSR102’, ‘6000’, ‘5000’, ‘1000’, 'A601’, 'E002’, 'DS05’);
INSERT INTO SpecificServiceRendered VALUES ('SSR103’, ‘4000’, ‘2500’, ‘1500’, 'A602’, 'E003’, 'DS01’);
INSERT INTO SpecificServiceRendered VALUES ('SSR104’, ‘330’, ‘250’, ‘80’, 'A603’, 'E003’, 'DS04’);
INSERT INTO SpecificServiceRendered VALUES ('SSR105’, ‘4500’, ‘3000’, ‘1500’, 'A604’, 'E005’, 'DS08’);
INSERT INTO SpecificServiceRendered VALUES ('SSR106’, ‘500’, ‘450’, ‘50’, 'A605’, 'E005’, 'DS09’);
INSERT INTO SpecificServiceRendered VALUES ('SSR107’, ‘480’, ‘480’, ‘0’, 'A606’, 'E004’, 'DS07’);
INSERT INTO SpecificServiceRendered VALUES ('SSR108’, ‘700’, ‘500’, ‘200’, 'A607’, 'E002’, 'DS06’);

INSERT INTO DentalService VALUES ('DS01’, ‘Dental Implants’, ‘4000’, ‘Dental Mirror, Drill Kit, Tissue Punch Kit, Anesthetic, Digital Caliper’);
INSERT INTO DentalService VALUES ('DS02’, ‘Tooth Extraction’, ‘300’, ‘Dental Extraction Forceps, Periosteal Elevator, Cotton Rolls’);
INSERT INTO DentalService VALUES ('DS03’, ‘Teeth Cleaning’, ‘200’, ‘Dental mirrors, Scalers, Perioprobes, Curettes, Polishers, Saliva Ejectors’);
INSERT INTO DentalService VALUES ('DS04’, ‘Dental Fillings’, ‘330’, ‘Dental Mirror, Dental Probe, Anaesthetic, Dental Syringe, Dental Drill, Spoon Excavator, Burnisher, Scaler’);
INSERT INTO DentalService VALUES ('DS05’, ‘Premium Dentures’, ‘6000’, ‘Denture Presses, Hydraulic Presses, Denture Curing Units, Boilout Units, Denture Compresses, Flas and Presses, Pressure Pots’);
INSERT INTO DentalService VALUES ('DS06’, ‘Gum Tissue Graft’, ‘700’, ‘Periodontal Probe, Orban Knife, Compator Packer, Tunneling Gum Lift, Lagrange Scissors, Scapel Handle, Elevator Allen’);
INSERT INTO DentalService VALUES ('DS07’, ‘Wisdom Teeth Removal’, ‘480’, ‘Extraction Forceps, Elevators, Scalpel, Surgical Bars, Needle Holders and Sutures’
INSERT INTO DentalService VALUES ('DS08’, ‘Metal Braces’, ‘4500’, ‘Spacers, Elastics, Rapid Palatial Dividers, Retainers’);
INSERT INTO DentalService VALUES ('DS09’, ‘Bit Correction’, ‘500’, ‘Ball Correction Bit’);
INSERT INTO DentalService VALUES ('DS10’, ‘Teeth Whitening’, ‘500’, ‘Carbamide peroxide, Hydrogen peroxide’);

INSERT INTO Employee VALUES ('E001’, ‘Lexi’, ‘ Mayo’, ‘97 Fenimore St’, ‘11225’, ‘Brooklyn’, NY’, ‘505-644-2646’, ‘leximayo01@gmail.com’, ‘Dentist’, ‘Salary’, ‘bi-weekly’);
INSERT INTO Employee VALUES ('E002’, ‘Romana’, ‘Collins’, ‘86 Buttonwood Rd’, ‘10304’, ‘Staten Island’, NY’, ‘407-295-3598’, ‘romanacollins10304@gmail.com’, ‘Dentist’, ‘Salary’, ‘bi-weekly’);
INSERT INTO Employee VALUES ('E003’, ‘Viktor’, ‘Faulkner’, ‘1601 W 11th St.’, ‘11204’, ‘Brooklyn’, NY’, ‘505-644-5730’, ‘faulknerviktor293@outlook.com’, ‘Dentist’, ‘Salary’, ‘bi-weekly’);
INSERT INTO Employee VALUES ('E004’, ‘Anoushka’, ‘Clay’, ‘104-71 43 Avenue’, ‘11368’, ‘Queens’, ‘NY’, ‘202-628-9770’, ‘anoushkaclay5243@gmail.com’, ‘Dentist’, ‘Salary’, ‘bi-weekly’);
INSERT INTO Employee VALUES ('E005’, ‘Jody’, ‘Hensley’, ‘5815 14th Ave’, ‘11219’, ‘Brooklyn’, NY’, ‘419-293-3034’, ‘jhensley1989@outlook.com’, ‘Orthodontist’, ‘Salary’, ‘bi-weekly’);
INSERT INTO Employee VALUES ('E006’, ‘Abubakr’, ‘Webster’, ‘72 Tennis Pl’, ‘11375’, ‘Queens’, ‘NY’, ‘512-407-8607’, ‘wabubakr72@outlook.com’, ‘Front Desk’, ‘Hourly’, ‘weekly’);
INSERT INTO Employee VALUES ('E007’, ‘Marshall’, ‘Bailey’, ‘327 E 63rd St’, ‘10065’, ‘Manhattan’, NY’, ‘319-943-2809’, ‘baileymarshall327@gmail.com’, ‘Dentist/Orthodontics Assistant’, ‘Hourly’, ‘weekly’);

INSERT INTO PaymentHistory VALUES ('PH601’, ‘11/18/2021 12:30:00 PM’, ‘Insurrence Covered’, ‘0’, ‘P101’
INSERT INTO PaymentHistory VALUES ('PH602’, ‘11/20/2021 06:00:00 PM’, ‘Credit Card’, ‘400’, ‘P102’
INSERT INTO PaymentHistory VALUES ('PH603’, ‘11/20/2021 08:30:00 PM’, ‘Personal Check’, ‘4000’, ‘P103’
INSERT INTO PaymentHistory VALUES ('PH604’, ‘11/30/2021 01:00:00 PM’, ‘Debit Card’, ‘250’, ‘P104’
INSERT INTO PaymentHistory VALUES ('PH605’, ‘12/14/2021 04:00:00 PM’, ‘Credit Card’, ‘650’, ‘P105’
INSERT INTO PaymentHistory VALUES ('PH606’, ‘12/22/2021 11:00:00 AM’, ‘Cash’, ‘50’, ‘P106’
INSERT INTO PaymentHistory VALUES ('PH607’, ‘01/04/2022 03:30:00 PM’, ‘Inssurence Covered’, ‘0’, ‘P107’
INSERT INTO PaymentHistory VALUES ('PH608’, ‘01/27/2022 05:30:00 PM’, ‘Debit Card’, ‘350’, ‘P108’

### Application Implentation

### Form #1

![image](https://github.com/Alvin-Liew/The-Local-Dentist-Clinic-Database/assets/105011531/50f16686-3e1a-4a42-b57b-3dfe24f61539)

The Employee Data Entry form includes all existing employees and allows for new employees to be entered. Employee Role, City, Pay Type, and Pay Time Period are all combo boxes. The form also has a VBA code to convert First and Last Names to proper cases.

### VBA Code:

![image](https://github.com/Alvin-Liew/The-Local-Dentist-Clinic-Database/assets/105011531/7937d54a-3043-4b69-87dc-955d6cc55cda)

### Form #2

![image](https://github.com/Alvin-Liew/The-Local-Dentist-Clinic-Database/assets/105011531/8536d29a-5139-4618-99b5-1703c086473f)

The Dental Service Data Entry form is used to look up all existing dental services and enter any new dental services the clinic may offer. The user can click the new service button to create a record and the save button to save the record. 

### Form #3

![image](https://github.com/Alvin-Liew/The-Local-Dentist-Clinic-Database/assets/105011531/7d69c0a4-2c32-4386-914b-6c24c1504331)

The Patient Data Entry form includes all existing patients made and allows for new patients to be added. The Insurance Coverage is a Combo box that includes the list of insurances accepted by the clinic. The form has several  VBA codes to convert First and Last Names to proper cases, a warning message when insurance is entered that is not accepted by the clinic, and generates a new and unique PatientID when double-clicked, creating a new record.

### VBA Code:

![image](https://github.com/Alvin-Liew/The-Local-Dentist-Clinic-Database/assets/105011531/f03cd04a-f9e2-4adb-9f53-f36212497574)

### Form #4

![image](https://github.com/Alvin-Liew/The-Local-Dentist-Clinic-Database/assets/105011531/2424c63f-8529-4304-baba-4173aaec75b1)

The Appointment Data Entry form includes all existing appointments made and allows for new appointments to be made. This form looks up patient data which can be helpful when creating appointments. The Insurance Coverage is a Combo box that includes the list of insurances accepted by the clinic. The form also has a VoBA code to convert First and Last Names to proper case.

### VBA Code:

![image](https://github.com/Alvin-Liew/The-Local-Dentist-Clinic-Database/assets/105011531/e728ca37-98b2-4085-95b3-309a1534ea31)

### Form #5

![image](https://github.com/Alvin-Liew/The-Local-Dentist-Clinic-Database/assets/105011531/4abaa559-d841-4c05-b2cd-d105f8a67216)

The Appointment Master form includes information from several tables. The Appointment table is the master with Patient lookup and SpecificSevericesRendered as detail with a lookup for Dental Service and Employee. This form can be helpful when creating a bill for the customer or for insurance. The form has VBA code to convert First and Last Names to proper cases and a warning message that payment is needed immediately when the amount_due surpasses $5,000. 

### VBA Code:

![image](https://github.com/Alvin-Liew/The-Local-Dentist-Clinic-Database/assets/105011531/6f2b6aae-61f9-44f6-a2de-66d1f4fdfe5f)

### Query #1

![image](https://github.com/Alvin-Liew/The-Local-Dentist-Clinic-Database/assets/105011531/f12545e4-eda6-4f20-8869-1f0f23e5652c)

### Report #1

![image](https://github.com/Alvin-Liew/The-Local-Dentist-Clinic-Database/assets/105011531/9bce82ff-24e5-41c8-bea0-45469e5e0cac)

This report shows the complete names and payment period/type of each employee

SQL:
SELECT Employee.Employee_ID, Employee.Firstname, Employee.Lastname, Employee.Paytype, Employee.PayTimePeriod
FROM Employee;

### Query #2

![image](https://github.com/Alvin-Liew/The-Local-Dentist-Clinic-Database/assets/105011531/2c26fd00-640a-4877-8cb4-e5c0ab4a45e3)

### Report #2

![image](https://github.com/Alvin-Liew/The-Local-Dentist-Clinic-Database/assets/105011531/96d46fd2-d726-417c-8548-f33bd5e4eeec)

This report shows the patient's name/address and appointment date so we can inform/update them of their upcoming appointment

SQL:
SELECT Patient.Patient_ID, Patient.Firstname, Patient.Lastname, Patient.Street, Patient.Zipcode, Patient.Phonenumber, Appointment.Appointment_DateTime
FROM Employee INNER JOIN (DentalService INNER JOIN (((Patient INNER JOIN Appointment ON Patient.Patient_ID = Appointment.Patient_ID) INNER JOIN PaymentHistory ON Patient.Patient_ID = PaymentHistory.Patient_ID) INNER JOIN SpecificServiceRendered ON Appointment.Appointment_ID = SpecificServiceRendered.Appointment_ID) ON DentalService.Dental_Service_ID = SpecificServiceRendered.Dental_Service_ID) ON Employee.Employee_ID = SpecificServiceRendered.Employee_ID;

### Query #3

![image](https://github.com/Alvin-Liew/The-Local-Dentist-Clinic-Database/assets/105011531/07edba9d-4ace-4c2d-be4c-45d96c087602)

### Report #3

![image](https://github.com/Alvin-Liew/The-Local-Dentist-Clinic-Database/assets/105011531/a9c2c8df-a5e1-4ef5-822d-a996a78503e2)

This report shows the total amount of money due from the patient and how much they spent already based on the number of appointments

SQL:
SELECT Patient.Patient_ID, Patient.Firstname, Patient.Lastname, Sum(PaymentHistory.Payment_Amount) AS TotalSpent, Count(Appointment.Appointment_ID) AS NumberOfAppointments, Sum(SpecificServiceRendered.Amount_Due) AS TotalAmountDue
FROM ((Patient INNER JOIN Appointment ON Patient.Patient_ID = Appointment.Patient_ID) INNER JOIN PaymentHistory ON Patient.Patient_ID = PaymentHistory.Patient_ID) INNER JOIN SpecificServiceRendered ON Appointment.Appointment_ID = SpecificServiceRendered.Appointment_ID
GROUP BY Patient.Patient_ID, Patient.Firstname, Patient.Lastname
ORDER BY Patient.Firstname, Patient.Lastname;

### Navigation Form:

![image](https://github.com/Alvin-Liew/The-Local-Dentist-Clinic-Database/assets/105011531/3d8328c0-2a23-4c1d-ae63-f8e0fc3f74ef)

The navigation form will pop up when the database opens and includes all the forms and reports.

## Conclusion

Developing this project has really shown the importance of databases and the development lifecycle. Our project implements all of the important steps to create the perfect model of a database. As a group to build this database we used a variety of software and services that included text via WhatsApp to communicate and coordinate activities. We also used software such as google docs to keep all of the data for the project organized, and Microsoft Access to bring the project to life. Our experience with this project was nothing short of beneficial and help with real-world examples. Learning hands-on going into a computer-based industry is very important but this project gave you the tools and knowledge to begin in such an industry. I think the most difficult steps in this project came into play with the database implementation. Writing the SQL create table statement was very tedious, but this was a major part of the project. It took a lot of correct coding to make sure all data was stored in tables correctly, and showing the examples which showed why a database was required in the first place, was again a lot of necessary work. Although this was the most difficult for us we used our knowledge and what we have learned in class to complete these steps. One of the easier steps we considered was logical and physical modeling. This is the foundation of the project which makes it very important. It was very straightforward because this was the first time we listed all functional dependencies and created the E-R model into a relational model. We also found that this part of the project was the most interesting as you can see the relationship between entities for the first time. Participating in this project has nonetheless shown us the importance of having a database within a company. Without a database keeping track of all records, a company would not be able to run as smoothly and would face big challenges down the road. It's actually very interesting to see how older companies operated without such a system in place. In all, this project has taught us the importance of having the skills to create databases, as this is something that will always be in demand for the workforce, and if we had the opportunity to do anything different we would not. We struggled in some parts and made other parts longer and harder than they should have been, but by failing and committing trial and error we feel as if our skills in creating an entire database became better. To conclude, as a group we realized the benefits of creating a database, and the importance it holds on the society and workforce that we live in today. 
