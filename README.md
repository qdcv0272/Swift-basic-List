# Swift-basic-List
<hr/>

<h3 align="center"> 🎥 시뮬레이터 🎥 </h3>

<p align="center"> 
  <img src="https://user-images.githubusercontent.com/91595135/159051029-85d61c45-08c6-4f36-87b3-2b691962c859.gif">
</p>
<hr/>

<h3 align="center">🔧 func review 🔧</h3>

<h4> 🚀tapAddButton🚀 </h4>
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







