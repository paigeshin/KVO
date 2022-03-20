# KVO

```swift

class BankAccount: NSObject {
    
    @objc dynamic var balance: Int = 0
    
    func deductAnnumalMaintenance() {
        balance -= 25
    }
    
    func depositAmount(amount: Int) {
        balance += amount
    }
    
    func withdrawAmount(amount: Int) {
        balance -= amount
    }
    
}

class Human: NSObject {
    
    @objc var myAccount: BankAccount = BankAccount()
    var observer: NSKeyValueObservation?
    
    func observeChangesInMyBalance() {
        self.observer = self.observe(\.myAccount.balance, options: [.old, .new]) { human, change in
            print(change)
        }
    }
    
    deinit {
        observer?.invalidate()
    }
    
}

let human: Human = Human()
human.observeChangesInMyBalance()
human.myAccount.deductAnnumalMaintenance()
// NSKeyValueObservedChange<Int>(kind: __C.NSKeyValueChange, newValue: Optional(-25), oldValue: Optional(0), indexes: nil, isPrior: false)
human.myAccount.depositAmount(amount: 300)
// NSKeyValueObservedChange<Int>(kind: __C.NSKeyValueChange, newValue: Optional(275), oldValue: Optional(-25), indexes: nil, isPrior: false)


```
