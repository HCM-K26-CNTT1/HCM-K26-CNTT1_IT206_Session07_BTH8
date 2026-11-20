# AI CODE REVIEWER – QUẢN LÝ SINH VIÊN C++

## 1. Mục tiêu

Sử dụng AI để đọc, phân tích, review và chấm điểm source code chương trình quản lý sinh viên theo Rubric 100 điểm.

Chương trình gồm 5 chức năng:
- Thêm sinh viên.
- Hiển thị danh sách.
- Tìm kiếm theo mã sinh viên.
- Xóa sinh viên.
- Tính điểm trung bình.

## 2. Rubric đánh giá 100 điểm

| Tiêu chí | Điểm tối đa |
|---|---:|
| Đúng chức năng nghiệp vụ | 30 |
| Cấu trúc Class và Object | 20 |
| Xử lý dữ liệu và ngoại lệ | 15 |
| Tổ chức code, khả năng đọc hiểu | 15 |
| Kiểm thử và xử lý tình huống biên | 20 |
| **Tổng** | **100** |

## 3. Source Code mẫu

File: `main.cpp`

```cpp
#include <iostream>
#include <vector>
using namespace std;

class Student {
public:
    string id, name;
    double score;

    Student(string i, string n, double s) {
        id = i;
        name = n;
        score = s;
    }

    void display() {
        cout << id << " - " << name
             << " - " << score << endl;
    }
};

class StudentManager {
private:
    vector<Student> students;

public:
    void addStudent() {
        string id, name;
        double score;

        cout << "Ma sinh vien: ";
        cin >> id;

        for (Student s : students) {
            if (s.id == id) {
                cout << "Ma da ton tai!\n";
                return;
            }
        }

        cout << "Ho ten: ";
        cin.ignore();
        getline(cin, name);

        cout << "Diem: ";
        cin >> score;

        if (score < 0 || score > 10) {
            cout << "Diem khong hop le!\n";
            return;
        }

        students.push_back(Student(id, name, score));
    }

    void displayStudents() {
        for (Student s : students)
            s.display();
    }

    void searchStudent() {
        string id;
        cout << "Nhap ma can tim: ";
        cin >> id;

        for (Student s : students) {
            if (s.id == id) {
                s.display();
                return;
            }
        }

        cout << "Khong tim thay!\n";
    }

    void deleteStudent() {
        string id;
        cout << "Nhap ma can xoa: ";
        cin >> id;

        for (int i = 0; i < students.size(); i++) {
            if (students[i].id == id) {
                students.erase(students.begin() + i);
                cout << "Da xoa!\n";
                return;
            }
        }

        cout << "Khong tim thay!\n";
    }

    void averageScore() {
        if (students.empty()) {
            cout << "Danh sach rong!\n";
            return;
        }

        double sum = 0;
        for (Student s : students)
            sum += s.score;

        cout << "Diem trung binh: "
             << sum / students.size() << endl;
    }
};

int main() {
    StudentManager manager;
    int choice;

    do {
        cout << "\n1. Them sinh vien";
        cout << "\n2. Hien thi";
        cout << "\n3. Tim kiem";
        cout << "\n4. Xoa sinh vien";
        cout << "\n5. Tinh diem trung binh";
        cout << "\n0. Thoat";
        cout << "\nLua chon: ";
        cin >> choice;

        switch (choice) {
            case 1: manager.addStudent(); break;
            case 2: manager.displayStudents(); break;
            case 3: manager.searchStudent(); break;
            case 4: manager.deleteStudent(); break;
            case 5: manager.averageScore(); break;
        }
    } while (choice != 0);

    return 0;
}
```

## 4. Prompt AI Code Reviewer

Bạn là chuyên gia review code C++. Hãy đọc source code tôi cung cấp và đánh giá theo Rubric 100 điểm bên dưới.

**Yêu cầu phân tích:**

1. Xác định các Class, Object và vai trò của chúng.
2. Kiểm tra 5 chức năng nghiệp vụ.
3. Đánh giá cấu trúc và chất lượng code.
4. Kiểm tra xử lý dữ liệu, ngoại lệ và tình huống biên.
5. Chấm điểm từng tiêu chí và giải thích.
6. Trích dẫn đoạn code làm minh chứng cho mỗi nhận xét.
7. Phân biệt lỗi cú pháp, lỗi logic và lỗi thiết kế.
8. Đề xuất cách sửa và thứ tự ưu tiên xử lý lỗi.

**Rubric cố định:**

- Chức năng nghiệp vụ: 30 điểm.
- Class và Object: 20 điểm.
- Dữ liệu và ngoại lệ: 15 điểm.
- Tổ chức code: 15 điểm.
- Kiểm thử và tình huống biên: 20 điểm.

**Quy định:**
- Không thay đổi điểm tối đa.
- Không chấm điểm chỉ dựa trên hình thức.
- Không có bằng chứng thì ghi chưa đủ cơ sở đánh giá.
- Không khẳng định chương trình chạy đúng nếu chưa thực thi.

**Định dạng kết quả:**

- Bảng chấm điểm chi tiết.
- Danh sách lỗi và mức độ nghiêm trọng (Critical, High, Medium, Low).
- Đoạn code minh chứng.
- Hướng sửa từng lỗi.
- Thứ tự ưu tiên sửa lỗi.
- Đánh giá tổng kết.

## 5. Lệnh thực hiện

**Bước 1: Biên dịch chương trình**

```bash
g++ -std=c++17 -Wall -Wextra -o main main.cpp
```

**Bước 2: Chạy chương trình**

```bash
./main
```

Windows PowerShell:

```powershell
.\main.exe
```

**Bước 3: Review bằng AI**

Upload `main.cpp` lên ChatGPT hoặc Gemini và gửi Prompt AI Code Reviewer ở mục 4.

**Bước 4: Cải thiện code**

Dựa trên danh sách lỗi AI phát hiện, sửa source code và thực hiện review lại.

## 6. So sánh trước và sau cải thiện

| Tiêu chí | Trước cải thiện | Sau cải thiện |
|---|---|---|
| Chức năng | Kiểm tra theo Rubric | Kiểm tra lại |
| Class và Object | Đánh giá thiết kế | Cải thiện cấu trúc |
| Xử lý dữ liệu | Tìm lỗi đầu vào | Bổ sung kiểm tra |
| Tổ chức code | Đánh giá khả năng đọc | Tối ưu code |
| Kiểm thử | Phát hiện tình huống thiếu | Bổ sung test |

AI Code Reviewer giúp đánh giá source code theo một bộ tiêu chí thống nhất, đưa ra bằng chứng cụ thể, phát hiện lỗi và đề xuất hướng cải thiện. Việc kết hợp AI với biên dịch và kiểm thử thực tế giúp nâng cao độ tin cậy của quá trình review code.
