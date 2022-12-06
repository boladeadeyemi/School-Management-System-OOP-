# School-Management-System-OOP-
School Management System
/*
 * SCHOOL MANAGEMENT SYSTEM PROJECT
 * Features
 * Add employee (Principal/Teacher) details.
 * Add Student details.
 * Add subject details.
 * Display salaries of employees.
 * Finding the number of students registered in  particular subject.
 */

// MAIN CLASS
class School {
  #studentArray;
  #teacherArray;
  #subjectArray;

  constructor() {
    this.#studentArray = [];
    this.#teacherArray = [];
    this.#subjectArray = [];
  }


  get teacherArray() {//JavaScript ES6 get Accessor
    return this.#teacherArray;
  }
  get studentArray() {//JavaScript ES6 get Accessor
    return this.#studentArray;
  }
  get subjectArray() {//JavaScript ES6 get Accessor
    return this.#subjectArray;
  }

  // 
  set teacherArray(teacher) {//JavaScript ES6 set Mutator
    this.#teacherArray.push(teacher);
  }
  set studentArray(student) {//JavaScript ES6 set Mutator
    this.#studentArray.push(student);
  }
  set subjectArray(subject) {//JavaScript ES6 set Mutator
    this.#subjectArray.push(subject);
  }
  //
  getTeacherSalary(name) {//Regular get method
    // this block shows the salary of the teacher name inputed
    for (let i = 0; i < this.#teacherArray.length; i++) {
      if ("_name" in this.#teacherArray[i]) {
        if (this.#teacherArray[i]["_name"] == name) {
          return this.#teacherArray[i]._basicSalary + this.#teacherArray[i]._livingExpenses + 20
        }
        return 'Teacher not found'
      }
    }
  }

  showSubjects() {
    let subjects = []
    for (let i = 0; i < this.#subjectArray.length; i++) {
      subjects.push(this.#subjectArray[i]["_subjectName"])
    }
    return subjects;
  }
}

class Employee extends School {
  constructor() {
    super();
    this._name;
    this._id;
    this._address;
    this._phoneNumber;
    this._email;
    this._basicSalary;
    this._livingExpenses;
  }

  get name() {//javascript ES6 get Accessor
    return this._name;
  }
  get id() {//javascript ES6 get Accessor
    return this._id;
  }
  get address() {//javascript ES6 get Accessor
    return this._address;
  }
  get phoneNumber() {//javascript ES6 get Accessor
    return this._phoneNumber;
  }
  get email() {//javascript ES6 get Accessor
    return this._email;
  }
  get basicSalary() {//javascript ES6 get Accessor
    return this._basicSalary;
  }
  getLivingExpenses() {//regular get method to get living Expenses dynamically
    return this._livingExpenses
  }

  // ***employee setter Accessor
  set name(input) {//javascript ES6 set Accessor
    this._name = input.toString();
  }
  set id(input) {//javascript ES6 set Accessor
    this._id = input.toString();
  }
  set address(input) {//javascript ES6 set Accessor
    this._address = input.toString();
  }
  set phoneNumber(input) {//javascript ES6 set Accessor
    this._phoneNumber = input.toString();
  }
  set email(input) {//javascript ES6 set Accessor
    this._email = input.toString();
  }
  set basicSalary(input) {//javascript ES6 set Accessor
    this._basicSalary = Number(input);
  }
  setLivingExpenses() {//regular set method to set living Expenses dynamically
    this._livingExpenses = Math.round((10 / 100) * this._basicSalary);
  }
}

// **principal class inherits from employee
class Principal extends Employee {
  constructor() {
    super();
    this._bonus
  }
  // **get bonus
  get bonus() {
    if (this._bonus == undefined) {
      return '"Please set principal bonus first"'
    } else {
      return this._bonus
    }

  }
  // set bonus
  set bonus(input) {
    this._bonus = Number(input);
  }
  // calculate principal salary
  get salary() {
    if (this._bonus == undefined) {
      return '"Please set principal bonus first"'
    }
    return this._basicSalary + this._livingExpenses + this._bonus;
  }
}
// **teacher class also inherits from employee
class Teacher extends Employee {
  constructor() {
    super();
    this._classNo
  }
  //calculate teacher salary
  get salary() {
    return this._basicSalary + this._livingExpenses + 20;
  }
}
// **Subject class
class Subject extends School {//Yet to understand this guy
  constructor() {//found how to implement this yet?
    super();
    this._subjectName;

  }
  // subject name getter
  get subjectName() {
    return this._subjectName;
  }
  // subject name setter
  set subjectName(input) {
    this._subjectName = input.toString();
  }
}

// **Student class
class Student extends Subject {
  constructor() {
    super();
    this._id;
    this._name;
    this._level;
  }
  //***student getters
  get id() {
    return this._id
  }
  get name() {
    return this._name
  }
  get level() {
    return this._level
  }

  //**student setters
  set id(input) {
    return this._id = input.toString()
  }
  set name(input) {
    return this._name = input.toString()
  }
  set level(input) {
    return this._level = input.toString()
  }
}
let school = new School();
let principal = new Principal();

/*
 * Main function
 * This function runs the program
 * Prompts user for actions they want to perform
 * returns (0)
*/
function main() {
  let mainOption
  do {
    alert("Main Menu \nPress 1. to add Employee \nPress 2. to add Student \nPress 3. to add Subject \nPress 4. Show subject \nPress 5. Show Employee's Salaries \nPress 6. Count Students \nPress 7. Exit \n");

    mainOption = Number(prompt("Select Option"));

    //ADD EMPLOYEE
    if (mainOption === 1) {
      alert("Employee Menu \nPress 1. Principal \nPress 2. Teacher \n");
      const employee = Number(prompt("Select Option"));

      if (employee === 1) {//Add Principal
        alert("Principal menu")
        principal.name = prompt("Enter Name");
        principal.id = prompt("Enter ID Number");
        principal.address = prompt("Enter Address");
        principal.phoneNumber = prompt("Enter Phone Number");
        principal.email = prompt("Enter Email");
        principal.basicSalary = prompt("Enter Basic Salary")
        principal.bonus = prompt('Enter Bonus')
        principal.setLivingExpenses()
        console.log("\n");
      }

      if (employee === 2) {//Add Teacher
        let teacher = new Teacher();
        alert("Teacher Menu")
        teacher.name = prompt("Enter Name");
        teacher.id = prompt("Enter ID Number");
        teacher.address = prompt("Enter Address");
        teacher.phoneNumber = prompt("Enter Phone Number");
        teacher.email = prompt("Enter Email");
        teacher.basicSalary = prompt("Enter Basic Salary");
        teacher.setLivingExpenses();
        school.teacherArray = teacher;
        console.log("\n");
      }
    }
    //ADD STUDENT
    if (mainOption === 2) {
      let student = new Student();
      alert("Student Menu")
      student.name = prompt("Enter student name");
      student.id = prompt("Enter student ID");
      student.level = prompt("Enter student level")
      school.studentArray = student;
    }

    // ADD SUBJECT
    if (mainOption === 3) {
      let subject = new Subject();
      alert("Subject Menu")
      subject.subjectName = prompt("Enter Subject Name")
      school.subjectArray = subject;
    }

    //SHOW SUBJECT
    if (mainOption === 4) {
      // alert("This Feature would be avialable soon \n")
      alert(school.showSubjects())

    }

    // SHOW EMPLOYEE SALARY
    if (mainOption === 5) {
      alert("Salary Menu \nPress 1. Principal \nPress 2. Teacher \n");
      const employeeOption = Number(prompt("Select Option"));
      if (employeeOption === 1) {//show principal salary
        if (principal.name == undefined) { alert('No Principal avialable') }
        else {
          alert(`Principal ${principal.name}'s Salary: $${principal.salary}`);
        }
      }
      if (employeeOption === 2) {//Show Teacher Salary
        // if(teacher.name == undefined){alert('No Teaher avialable')}
        // else {
        // alert(`Teacher ${teacher.name}'s Salary: $${teacher.salary}`);
        // }
        const teacherName = prompt("Enter Teacher's name")
        if (school.getTeacherSalary(teacherName) == undefined) {
          alert("Teacher not found")
        }
        else {
          alert(`${teacherName}'s Salary:  $${school.getTeacherSalary(teacherName)}`)
        }

      }
      console.log("\n");
    }

    //COUNT STUDENTS IN SUBJECT
    if (mainOption === 6) {
      if (school.studentArray.length <= 1) {
        alert(`${school.studentArray.length} Student`)
      } else {
        alert(`${school.studentArray.length} Students`)
      }
    }

    // EXIT APP
    if (mainOption === 7) return 0 //this returns 0 and exits
  }
  while (mainOption != 7)
}
main();


