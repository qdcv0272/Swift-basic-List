# Swift-basic-List
<hr/>

<h3 align="center"> ๐ฅ ์๋ฎฌ๋ ์ดํฐ ๐ฅ </h3>

<p align="center"> 
  <img src="https://user-images.githubusercontent.com/91595135/159051029-85d61c45-08c6-4f36-87b3-2b691962c859.gif">
</p>
<hr/>

<h3 align="center">๐ง func review ๐ง</h3>

<h4 align="center"> ๐tapAddButton๐ </h4>
Add ๋ฒํผ์ ๋๋ ์๋ ํ ์ผ์ ๋ฑ๋กํ ์ ์๋ alert ํ์

```swift

@IBAction func tapAddButton(_ sender: UIBarButtonItem) {
    let alert = UIAlertController(title: "To do List!", message: nil, preferredStyle: .alert)
    let registerButton = UIAlertAction(title: "๋ฑ๋ก", style: .default, handler: { [weak self] _ in
      guard let title = alert.textFields?[0].text else {return}
      let task = Task(title: title, done: false)
      self?.tasks.append(task)
      self?.tableView.reloadData()
    })
    let cancelButton = UIAlertAction(title: "์ทจ์", style: .cancel, handler: nil)
    alert.addAction(cancelButton)
    alert.addAction(registerButton)
    alert.addTextField(configurationHandler: { textField in
      textField.placeholder = "ํ  ์ผ์ ์๋ ฅํด์ฃผ์ธ์ !"
    })
    
    self.present(alert, animated: true, completion: nil)
  }

```

<hr/>
<h4 align="center"> ๐ UITableViewDataSourece ๐ </h4>
UITableViewDataSourece ๋ ํ์ด๋ธ ๋ทฐ๋ฅผ ์์ฑํ๊ณ  ์์ ํ๋๋ฐ ํ์ํ ์ ๋ณด๋ฅผ ํ์ด๋ธ ๋ทฐ ๊ฐ์ณ ์ ๊ณต </br></br>


*ํ์์์ฑ*

```swift
func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    return self.tasks.count
  }
```


numberOfRowsInSection : ๊ฐ ์์์ ํ์ํ  ํ์ ๊ฐ์๋ฅผ ๋ฌป๋ ๋ฉ์๋ </br>
cellForRowAt : ํน์  ์ธ๋ฑ์ค Row์ Cell์ ๋ํ ์ ๋ณด๋ฅผ ๋ฃ์ด Cell ์ ๋ฐํํ๋ ๋ฉ์๋ </br>

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

*์ฌ์ฉํ ๋ฉ์๋*

commit: ํธ์ง ๋ชจ๋์์ ์ญ์ ๋ฒํผ์ ๋๋ ์๋ cell ์ด tableView ์ ์๋ ํ ์ผ ๋ค์ด ์ญ์ 

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

<h4 align="center"> ๐ UITableViewDelgate ๐ </h4>
UITableViewDelgate ๋ ํ์ด๋ธ ๋ทฐ์ผ ์๊ฐ์ ์ด ๋ถ๋ถ์ ์ค์ , ํ์ ์ก์ ๊ด๋ฆฌ, ์์ธ์๋ฆฌ ์ง์ ๊ฐ๋ณ ํ ํธ์ง์ ๋์์ค </br>

```swift
func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
    var task = self.tasks[indexPath.row]
    task.done = !task.done
    self.tasks[indexPath.row] = task
    self.tableView.reloadRows(at: [indexPath], with: .automatic)
  }
```

didSelectRowAt: ํ์ด ์ ํ๋์์๋ ํธ์ถ๋๋ ๋ฉ์๋
