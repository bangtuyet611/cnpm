
# cnpmflowchart TB
    %% Định nghĩa Actors
    SV[/"👤 Sinh viên"\]
    GV[/"👤 Giảng viên"\]
    HTTT[/"🏦 Hệ thống Thanh toán"\]
    
    %% Định nghĩa System Boundary
    subgraph SYSTEM["🎓 HỆ THỐNG ĐĂNG KÝ HỌC PHẦN TRỰC TUYẾN"]
        direction TB
        
        %% Use Case chung
        UC_Login(("Đăng nhập"))
        
        %% Use Cases của Sinh viên
        UC_ViewCourses(("Xem danh sách<br/>học phần"))
        UC_ViewDetails(("Xem chi tiết<br/>học phần"))
        UC_Register(("Đăng ký<br/>học phần"))
        UC_Payment(("Thanh toán<br/>học phí"))
        UC_ViewSchedule(("Xem lịch học"))
        UC_AddCourse(("Thêm học phần"))
        UC_DropCourse(("Hủy học phần"))
        UC_ViewGrades(("Xem điểm"))
        
        %% Use Cases của Giảng viên
        UC_ViewTeachingClasses(("Xem danh sách<br/>lớp giảng dạy"))
        UC_ViewStudents(("Xem danh sách<br/>sinh viên"))
        UC_EnterGrades(("Nhập điểm"))
        
        %% Use Cases tự động
        UC_CancelClass(("Hủy lớp<br/>thiếu sĩ số"))
        UC_TransferAlternative(("Chuyển sang<br/>học phần thay thế"))
    end
    
    %% Associations - Sinh viên
    SV --- UC_ViewCourses
    SV --- UC_ViewDetails
    SV --- UC_Register
    SV --- UC_ViewSchedule
    SV --- UC_AddCourse
    SV --- UC_DropCourse
    SV --- UC_ViewGrades
    
    %% Associations - Giảng viên
    GV --- UC_ViewTeachingClasses
    GV --- UC_ViewStudents
    GV --- UC_EnterGrades
    
    %% Associations - Hệ thống Thanh toán
    UC_Payment --- HTTT
    
    %% Include relationships
    UC_ViewCourses -.->|"<<include>>"| UC_Login
    UC_ViewDetails -.->|"<<include>>"| UC_Login
    UC_Register -.->|"<<include>>"| UC_Login
    UC_ViewSchedule -.->|"<<include>>"| UC_Login
    UC_AddCourse -.->|"<<include>>"| UC_Login
    UC_DropCourse -.->|"<<include>>"| UC_Login
    UC_ViewGrades -.->|"<<include>>"| UC_Login
    UC_ViewTeachingClasses -.->|"<<include>>"| UC_Login
    UC_ViewStudents -.->|"<<include>>"| UC_Login
    UC_EnterGrades -.->|"<<include>>"| UC_Login
    
    UC_Register -.->|"<<include>>"| UC_Payment
    
    %% Extend relationships
    UC_ViewDetails -.->|"<<extend>>"| UC_ViewCourses
    UC_TransferAlternative -.->|"<<extend>>"| UC_CancelClass
    
    %% Styling
    classDef actorStyle fill:#e1f5ff,stroke:#01579b,stroke-width:3px,color:#000
    classDef usecaseStyle fill:#fff9c4,stroke:#f57f17,stroke-width:2px,color:#000
    classDef systemStyle fill:#f3e5f5,stroke:#4a148c,stroke-width:3px,color:#000
    
    class SV,GV,HTTT actorStyle
    class UC_Login,UC_ViewCourses,UC_ViewDetails,UC_Register,UC_Payment,UC_ViewSchedule,UC_AddCourse,UC_DropCourse,UC_ViewGrades,UC_ViewTeachingClasses,UC_ViewStudents,UC_EnterGrades,UC_CancelClass,UC_TransferAlternative usecaseStyle
