# 変えるとこ
変更するとこをメソッドごとに書いてる。メソッドの中をそれぞれ確認して書き換えるor書き足すこと。

### １ピンの色変えて保存
投稿画面

```swift:

class ViewController2{

	var mapAnnotationView:MKPinAnnotationView = MKPinAnnotationView()

	@IBAction func testUISwitch(sender: UISwitch) {

		print("changeSwitch")

		if ( sender.isOn ) {
			//testLabel.text = "行った"
			mapAnnotationView.pinTintColor = UIColor.green
			} else {
				//testLabel.text = "これから"
				mapAnnotationView.pinTintColor = UIColor.blue
			}
		}
	}

	func mapView(_ mapView: MKMapView, viewFor annotation: MKAnnotation) -> MKAnnotationView? {

		let pinView = MKPinAnnotationView()
		if ( dataSwitch.isOn ) {
			//testLabel.text = "行った"
			pinView.pinTintColor = UIColor.green
			} else {
				//testLabel.text = "これから"
				pinView.pinTintColor = UIColor.blue
			}

			mapAnnotationView = pinView

			return mapAnnotationView
		}


	}


```

### ２キーボード最初から出すのやめる
投稿画面

```swift

class ViewController2{
	func viewDidLoad(){
		self.textfield.becomeFirstResponder()  //これを消す
	}
}

```

### ３ピンタップしたらセルに飛ぶ
これはmapの方ね

```swift

class ViewController{
	override func viewDidLoad() {
		mapView.delegate = self			//書き足す
	}

	//書き足す。これ入れると自動更新されるようになる
	override func viewWillAppear(_ animated: Bool) {
        readKiwamiData()
        mapView.reloadInputViews()
    }

}

```

### ４絵文字３つまでに制限する
投稿画面

```swift
class ViewController2{
	func backSpaceButtonImage(for emojiKeyboardView: AGEmojiKeyboardView!) -> UIImage! {
		return "🔙".image()
	}


	//キーボードの動きを見るところ。ここでtextfieldとかに文字を入れる
	func emojiKeyBoardView(_ emojiKeyBoardView: AGEmojiKeyboardView!, didUseEmoji emoji: String!) {
		if (textfield.text?.characters.count)! <= 2{
			self.textfield.text?.append(emoji)
		}

	}

	//ここも必ずかくこと。空っぽでもこのメソッドないとエラーでる
	func emojiKeyBoardViewDidPressBackSpace(_ emojiKeyBoardView: AGEmojiKeyboardView!) {
		if (textfield.text?.characters.count)! >= 1{
			var str:String = self.textfield.text!
			str = str.substring(to: str.index(before: str.endIndex))
			self.textfield.text = str
		}

	}

}

```

### ５セルの中のレイアウトとデザイン改良する
がんば！
