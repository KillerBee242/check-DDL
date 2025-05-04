# Data Definition Language : Society

CREATE TABLE Department (
    Num_S INT PRIMARY KEY,
    Label VARCHAR(255) NOT NULL,
    Manager_Name VARCHAR(255)
);

CREATE TABLE Employee (
    Num_E INT PRIMARY KEY,
    Name VARCHAR(255) NOT NULL,
    Position VARCHAR(255),
    Salary DECIMAL(10, 2) CHECK (Salary >= 0),
    Department_Num_S INT NOT NULL,
    
    CONSTRAINT fk_employee_department
    	FOREIGN KEY (Department_Num_S)
    	REFERENCES Department (Num_S)
    	ON DELETE RESTRICT
    	ON UPDATE CASCADE
);

CREATE TABLE Project (
    Num_P INT PRIMARY KEY,
    Title VARCHAR(255) NOT NULL,
    Start_Date DATE,
    End_Date DATE,
    Department_Num_S INT NOT NULL,
    
    CONSTRAINT fk_project_department
    	FOREIGN KEY (Department_Num_S)
    	REFERENCES Department (Num_S)
    	ON DELETE RESTRICT
    	ON UPDATE CASCADE
);

CREATE TABLE Employee_Project (
    Employee_Num_E INT NOT NULL,
    Project_Num_P INT NOT NULL,
    Role VARCHAR(255) NOT NULL,
    
    PRIMARY KEY (Employee_Num_E, Project_Num_P),
    
    CONSTRAINT fk_ep_employee
    	FOREIGN KEY (Employee_Num_E)
    	REFERENCES Employee (Num_E)
    	ON DELETE CASCADE,
    
    CONSTRAINT fk_ep_project
    	FOREIGN KEY (Project_Num_P)
    	REFERENCES Project (Num_P)
    	ON DELETE CASCADE
);

CREATE INDEX idx_employee_dept ON Employee(Department_Num_S);
CREATE INDEX idx_project_dept ON Project(Department_Num_S);
CREATE INDEX idx_ep_project ON Employee_Project(Project_Num_P);
