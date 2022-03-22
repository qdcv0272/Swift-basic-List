# Swift-basic-List
<hr/>

<h3 align="center"> 🎥 시뮬레이터 🎥 </h3>

<p align="center"> 
  <img src="https://user-images.githubusercontent.com/91595135/159051029-85d61c45-08c6-4f36-87b3-2b691962c859.gif">
</p>
<hr/>

<h3 align="center">🔧 func review 🔧</h3>

<h4 align="center"> 🚀tapAddButton🚀 </h4>
Add 버튼을 눌렀을때 할일을 등록할수 있는 alert 표시

```swift

@IBAction func tapAddButton(_ sender: UIBarButtonItem) {
    let alert = UIAlertController(title: "To do List!", message: nil, preferredStyle: .alert)
    let registerButton = UIAlertAction(title: "등록", style: .default, handler: { [weak self] _ in
      guard let title = alert.textFields?[0].text else {return}
      let task = Task(title: title, done: false)
      self?.tasks.append(task)
      self?.tableView.reloadData()
    })
    let cancelButton = UIAlertAction(title: "취소", style: .cancel, handler: nil)
    alert.addAction(cancelButton)
    alert.addAction(registerButton)
    alert.addTextField(configurationHandler: { textField in
      textField.placeholder = "할 일을 입력해주세요 !"
    })
    
    self.present(alert, animated: true, completion: nil)
  }

```

<hr/>
<h4 align="center"> 🚀 UITableViewDataSourece 🚀 </h4>
UITableViewDataSourece 는 테이블 뷰를 생성하고 수정하는데 필요하 정보를 테이블 뷰 객쳉 제공 </br></br>


*필수속성*

```swift
func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    return self.tasks.count
  }
```


numberOfRowsInSection : 각 색션에 표시할 행의 개수를 묻는 메서드 </br>
cellForRowAt : 특정 인덱스 Row의 Cell에 대한 정보를 넣어 Cell 을 반환하는 메서드 </br>

```swift
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    let cell = tableView.dequeueReusableCell(withIdentifier: "Cell", for: indexPath)
    let task = self.tasks[indexPath.row]
    cell.textLabel?.text = task.title
    
    if task.done {
      cell.accessoryType = .checkmark
    } else {
      cell.accessoryType = .none
    }
    return cell
  }
```
<hr/>

*사용한 메서드*

commit: 편집 모드에서 삭제버튼을 눌렀을때 cell 이 tableView 에 있는 할일 들이 삭제

```swift
func tableView(_ tableView: UITableView, commit editingStyle: UITableViewCell.EditingStyle, forRowAt indexPath: IndexPath) {
    self.tasks.remove(at: indexPath.row)
    tableView.deleteRows(at: [indexPath], with: .automatic)
    
    if self.tasks.isEmpty {
      self.doneButtonTap()
    }
  }
```

<hr/>

<h4 align="center"> 🚀 UITableViewDelgate 🚀 </h4>
UITableViewDelgate 는 테이블 뷰으 시각적이 부분을 설정, 행의 액션 관리, 엑세서리 지원 개별 행 편집을 도와줌 </br>

```swift
func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
    var task = self.tasks[indexPath.row]
    task.done = !task.done
    self.tasks[indexPath.row] = task
    self.tableView.reloadRows(at: [indexPath], with: .automatic)
  }
```

didSelectRowAt: 행이 선택되었을때 호출되는 메서드
