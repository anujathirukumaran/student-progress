# Sample Data for Testing

## Test Accounts

### Teacher Accounts

**Teacher 1 - Computer Science**
```
Name: John Smith
Email: john.teacher@test.com
Password: teacher123
Role: Staff
Department: Computer Science
```

**Teacher 2 - Mathematics**
```
Name: Sarah Johnson
Email: sarah.teacher@test.com
Password: teacher123
Role: Staff
Department: Mathematics
```

**Teacher 3 - Physics**
```
Name: Michael Brown
Email: michael.teacher@test.com
Password: teacher123
Role: Staff
Department: Physics
```

### Student Accounts

**Student 1**
```
Name: Alice Williams
Email: alice.student@test.com
Password: student123
Role: Student
```

**Student 2**
```
Name: Bob Davis
Email: bob.student@test.com
Password: student123
Role: Student
```

**Student 3**
```
Name: Charlie Wilson
Email: charlie.student@test.com
Password: student123
Role: Student
```

**Student 4**
```
Name: Diana Martinez
Email: diana.student@test.com
Password: student123
Role: Student
```

## Sample Progress Data

### For Alice Williams (Computer Science)

**Attendance:**
- Total Classes: 50
- Attended Classes: 47
- Percentage: 94%

**Marks:**
1. Data Structures
   - Marks: 85/100
   - Exam Type: Mid-term
   - Date: Current date

2. Algorithms
   - Marks: 92/100
   - Exam Type: Mid-term
   - Date: Current date

3. Database Management
   - Marks: 88/100
   - Exam Type: Quiz
   - Date: Current date

4. Web Development
   - Marks: 95/100
   - Exam Type: Assignment
   - Date: Current date

**Suggestions:**
- "Excellent performance in Web Development. Keep up the good work!"
- "Focus more on time complexity in Algorithms."
- "Great attendance record. Very consistent."

**Overall Performance:** Excellent

### For Bob Davis (Computer Science)

**Attendance:**
- Total Classes: 50
- Attended Classes: 38
- Percentage: 76%

**Marks:**
1. Data Structures
   - Marks: 65/100
   - Exam Type: Mid-term

2. Algorithms
   - Marks: 70/100
   - Exam Type: Mid-term

3. Database Management
   - Marks: 72/100
   - Exam Type: Quiz

**Suggestions:**
- "Need to improve attendance. Missing too many classes."
- "Good effort in recent assignments. Keep improving."
- "Consider attending extra help sessions."

**Overall Performance:** Average

### For Charlie Wilson (Mathematics)

**Attendance:**
- Total Classes: 45
- Attended Classes: 42
- Percentage: 93.33%

**Marks:**
1. Calculus I
   - Marks: 90/100
   - Exam Type: Mid-term

2. Linear Algebra
   - Marks: 88/100
   - Exam Type: Mid-term

3. Statistics
   - Marks: 85/100
   - Exam Type: Quiz

**Suggestions:**
- "Strong mathematical foundation. Excellent work!"
- "Consider participating in math competitions."

**Overall Performance:** Excellent

### For Diana Martinez (Physics)

**Attendance:**
- Total Classes: 48
- Attended Classes: 40
- Percentage: 83.33%

**Marks:**
1. Mechanics
   - Marks: 78/100
   - Exam Type: Mid-term

2. Thermodynamics
   - Marks: 82/100
   - Exam Type: Mid-term

3. Electromagnetism
   - Marks: 75/100
   - Exam Type: Quiz

**Suggestions:**
- "Good understanding of concepts. Practice more problems."
- "Attendance could be better. Try not to miss classes."

**Overall Performance:** Good

## Testing Scenarios

### Scenario 1: Complete Teacher Workflow
1. Register as teacher (Computer Science department)
2. Login to teacher dashboard
3. See list of all students
4. Click "Edit Progress" on Alice Williams
5. Add attendance: 50 total, 47 attended
6. Add marks: Data Structures, 85/100, Mid-term
7. Add suggestion: "Excellent performance!"
8. Set overall performance: Excellent
9. Click "Update Progress"
10. Verify success message

### Scenario 2: Student View Workflow
1. Register as student (Alice Williams)
2. Login to student dashboard
3. Initially see "No Progress Data Available"
4. After teacher adds data, refresh page
5. View attendance summary (94%)
6. View marks table with all subjects
7. Read teacher suggestions
8. See overall performance rating
9. Verify cannot edit anything

### Scenario 3: Multiple Students Management
1. Login as teacher
2. Add progress for multiple students
3. View login/logout times for each student
4. Filter students by department
5. Update existing student progress
6. Add new marks to existing records

### Scenario 4: Cross-Department Testing
1. Create teacher in Computer Science
2. Create teacher in Mathematics
3. Create students
4. CS teacher adds data for students
5. Math teacher adds data for same students
6. Verify each teacher sees only their department data
7. Students see all their progress data

## API Testing with Postman/Thunder Client

### Register User
```
POST http://localhost:5000/api/auth/register
Content-Type: application/json

{
  "name": "Test User",
  "email": "test@example.com",
  "password": "password123",
  "role": "student"
}
```

### Login
```
POST http://localhost:5000/api/auth/login
Content-Type: application/json

{
  "email": "test@example.com",
  "password": "password123"
}
```

### Get Student Progress (Student)
```
GET http://localhost:5000/api/progress/my-progress
Authorization: Bearer YOUR_JWT_TOKEN
```

### Update Student Progress (Teacher)
```
PUT http://localhost:5000/api/progress/student/STUDENT_ID
Authorization: Bearer YOUR_JWT_TOKEN
Content-Type: application/json

{
  "attendance": {
    "totalClasses": 50,
    "attendedClasses": 47
  },
  "marks": [{
    "subject": "Mathematics",
    "marks": 85,
    "maxMarks": 100,
    "examType": "Mid-term",
    "date": "2024-01-15"
  }],
  "suggestions": "Great work! Keep it up.",
  "overallPerformance": "Excellent"
}
```

### Get All Students (Teacher)
```
GET http://localhost:5000/api/progress/students
Authorization: Bearer YOUR_JWT_TOKEN
```

## Performance Ratings

Use these standard ratings:
- **Excellent**: 90%+ attendance, 85%+ average marks
- **Good**: 80-89% attendance, 75-84% average marks
- **Average**: 70-79% attendance, 65-74% average marks
- **Needs Improvement**: Below 70% attendance or below 65% marks

## Departments List

Suggested departments for testing:
- Computer Science
- Mathematics
- Physics
- Chemistry
- Biology
- English
- History
- Economics
- Mechanical Engineering
- Electrical Engineering

## Testing Checklist

- [ ] Register multiple teachers with different departments
- [ ] Register multiple students
- [ ] Teacher adds attendance for students
- [ ] Teacher adds marks for multiple subjects
- [ ] Teacher adds suggestions
- [ ] Teacher sets overall performance
- [ ] Student views their progress
- [ ] Student cannot edit data
- [ ] Login/logout times are tracked
- [ ] Department filtering works
- [ ] Data persists after logout
- [ ] Responsive design on mobile
- [ ] All API endpoints work correctly

## Common Test Cases

### Positive Tests
✅ Valid registration
✅ Valid login
✅ Teacher can update student progress
✅ Student can view their progress
✅ Attendance percentage calculates correctly
✅ Marks display properly
✅ Suggestions appear in order

### Negative Tests
❌ Register with existing email (should fail)
❌ Login with wrong password (should fail)
❌ Student tries to edit data (should be read-only)
❌ Access protected route without token (should fail)
❌ Teacher tries to access another department's students (should filter)

## Tips for Testing

1. **Use Browser DevTools**: Check Network tab for API calls
2. **Check Console**: Look for any JavaScript errors
3. **Test Responsiveness**: Use device toolbar in DevTools
4. **Clear LocalStorage**: Test fresh login experience
5. **Test Edge Cases**: Empty data, large numbers, special characters
6. **Cross-Browser Testing**: Test on Chrome, Firefox, Safari
7. **Mobile Testing**: Test on actual mobile devices

## Sample Feedback Messages

**Positive:**
- "Outstanding performance! Keep up the excellent work."
- "Great improvement from last assessment."
- "Your dedication is showing in your results."
- "Excellent attendance and participation."

**Constructive:**
- "Focus more on understanding core concepts."
- "Try to improve attendance for better learning."
- "Practice more problems to strengthen fundamentals."
- "Consider attending extra help sessions."

**Encouraging:**
- "Good progress! Keep working hard."
- "You're on the right track. Stay consistent."
- "Nice improvement! Continue this momentum."
- "Your effort is appreciated. Keep it up."
