---
layout: default
title: java null check
parent: java
nav_order: 201108
---

```java
public class NullCheck {
    private class School {
        private ClassRoom classRoom;

        public ClassRoom getClassRoom() {
            return classRoom;
        }
    }

    private class ClassRoom {
        private Student student;

        public Student getStudent() {
            return student;
        }
    }

    private class Student {

    }
    
    // 깊은 의심 패턴
    public void deepDoubtPattern(School school) {
        if (school != null) {
            if (school.getClassRoom() != null) {
                Student student = school.getClassRoom().getStudent();
            }
        }
    }

    // Optional의 map을 사용한 null check 및 object 가져오기
    public void useOptional(School school) {
        Student student = Optional.ofNullable(school)
                .map(School::getClassRoom)
                .map(ClassRoom::getStudent)
                .orElse(null);
    }

}
```

### 참고링크
* https://multifrontgarden.tistory.com/131
