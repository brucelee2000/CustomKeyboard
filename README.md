# CustomKeyboard
Custom keyboard is achieved by making an Application Extention.
* **Step 1. Make a new single View application**
* **Step 2. Make a new target and choose custom keyboard from Application**

Add a button to switch among keyboards
--------------------------------------
**Add a button with the action of "*advanceToNextInputMode*"**

        @IBOutlet var nextKeyboardButton: UIButton!
    
        override func updateViewConstraints() {
            super.updateViewConstraints()
        
            // Add custom view sizing constraints here
        }
    
        override func viewDidLoad() {
            super.viewDidLoad()

            self.nextKeyboardButton = UIButton.buttonWithType(.System) as! UIButton
        
            self.nextKeyboardButton.setTitle(NSLocalizedString("Next Keyboard", comment: "Title for 'Next Keyboard' button"), forState: .Normal)
            self.nextKeyboardButton.sizeToFit()
            self.nextKeyboardButton.setTranslatesAutoresizingMaskIntoConstraints(false)
        
            self.nextKeyboardButton.addTarget(self, action: "advanceToNextInputMode", forControlEvents: .TouchUpInside)
            
            self.view.addSubview(self.nextKeyboardButton)
        
            var nextKeyboardButtonLeftSideConstraint = NSLayoutConstraint(item: self.nextKeyboardButton, attribute: .Left, relatedBy: .Equal, toItem: self.view, attribute: .Left, multiplier: 1.0, constant: 0.0)
            var nextKeyboardButtonBottomConstraint = NSLayoutConstraint(item: self.nextKeyboardButton, attribute: .Bottom, relatedBy: .Equal, toItem: self.view, attribute: .Bottom, multiplier: 1.0, constant: 0.0)
            self.view.addConstraints([nextKeyboardButtonLeftSideConstraint, nextKeyboardButtonBottomConstraint])
        }

Add a button with corresponding action in the keyboard
------------------------------------------------------
* **Step 1. Add a button to the keyboard**

        // Add a customized button
        let button = UIButton.buttonWithType(.System) as! UIButton
        button.frame = CGRectMake(150, 40, 100, 120)
        
        var cat = UIImage(named: "cat2.jpg")
        button.setBackgroundImage(cat, forState: .Normal)
        
        button.addTarget(self, action: "buttonPressed", forControlEvents: .TouchUpInside)
    
        self.view.addSubview(button)
        
* **Step 2. Add its action to the button by using "*textDocumentProxy*"**

        func buttonPressed() {
            // A proxy to the text input object that the custom keyboard is interacting with. (read-only)
            var proxy = textDocumentProxy as! UITextDocumentProxy
    
            // What text to be inserted into the displayed text when button is pressed.
            proxy.insertText("meow~~~")
            
        }
