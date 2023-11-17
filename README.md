<img width="825" alt="image" src="https://github.com/shlim0/ios-bank-manager/assets/142188004/d1199a03-9774-4daa-9d6b-8a88a0691286">








### 프로젝트 참여자 🤝

| <img src="https://avatars.githubusercontent.com/u/142188004?v=4" width="90" height="90"> | <img src="https://avatars.githubusercontent.com/u/46235301?v=4" width="90" height="90"> |
| ----------- | --------- |
| [@SimJaeHyeok](https://github.com/SimJaeHyeok) | [@shlim0](https://github.com/shlim0) |
| JaeHyeok | Jjong |

</br>

### UML

---

```mermaid
classDiagram
    class Node {
        + data: T << read-only >>
        + next: Node<T>?
    }

    class Queue {
        - head: Node<T>?
        - tail: Node<T>?
        + enqueue(data: T)
        + dequeue(): T?
        + clear()
        + peek(): T?
        + isEmpty(): Bool
    }

    class Customer {
        + id: Int << read-only >>
		    + task: Taskable.Type << read-only >>
    }

    class BankViewController {
        - bankView: BankView << read-only >>
				- timer: Timer
				- elaspedTime: TimeInterval
				- bank: Bank
				- startTimer()
				- updateTimer()
				- startBank()
				- reset()
				+ addWaitingStackView(_ bank: Bank, _ customer: Customer)
				+ addWorkingStackView(_ banker: Banker, _ customer: Customer)
				+ deleteWorkingStackView(_ banker: Banker, _ customer: Customer)
    }

		class BankView {
				- setConstraint()
				- setContentStackViewConstraint()
				- setWaitingStackViewConstraint()
				- setWorkingStackViewConstraint()
				+ updateTime(_ minutes: Int, _ seconds: Int, _ milliseconds: Int)
				+ add(_ customer: Customer, to stackView: UIStackView)
				+ delete(_ customer: Customer, from stackView: UIStackView)
				+ resetWorkingTimeLabel()
				+ resetCustomer()
		}

		class BankDelegate {
				<< protocol >>
				+ addWaitingStackView(_ bank: Bank, _ customer: Customer)
		}

		class BankerDelegate {
				<< protocol >>
		    + addWorkingStackView(_ banker: Banker, _ customer: Customer)
		    + deleteWorkingStackView(_ banker: Banker, _ customer: Customer)
}

    class Bank {
				- bankerDelegate: BankerDelegate?
				- bankDelegate: BankDelegate?
        - queueManager: QueueManager
        - banker: Banker
        - totalCustomerCount: Int
				- elapsedTime: Double
				- isReset: Bool
        + greetCustomer()
        + startWork()
				+ prepareCloseWork()
				- insert(_ customer: Customer, _ group: DispatchGroup)
				- selectRandomTask(): Taskable.Type
    }

    class Banker {
				+ work(_ delegate: BankerDelegate?, for customer: Customer, _ isReset: Bool)
    }

    class QueueManager {
        - queue: Queue<Customer>
        + getQueue(): Queue<Customer>
        + clearQueue()
    }

		class Taskable {
		<< protocol >>
				+ name: String << static >>
				+ semaphore: DispatchSemaphore << static >>
				+ processingTime: Double << static >>
		}

		class DepositTask {
				+ name: String << static / read-only >>
				+ semaphore: DispatchSemaphore << static / read-only >>
				+ processingTime: Double << static / read-only>>
		}

		class LoanTask {
				+ name: String << static / read-only >>
				+ semaphore: DispatchSemaphore << static / read-only >>
				+ processingTime: Double << static / read-only>>
		}

    Node --* Queue : contains
		Queue --* QueueManager
    QueueManager --> Customer : contains
    QueueManager --* Bank : manages
		Customer --* Bank
		Banker --* Bank
		Banker --> Customer : interact with
		Bank --* BankViewController : manages
		Bank --> Taskable
		BankViewController --* main
		BankViewController ..|> BankDelegate
		BankViewController ..|> BankerDelegate
		BankView --* BankViewController
		Customer --> Taskable
		DepositTask ..|> Taskable
		LoanTask ..|> Taskable
```

### 구동 화면📱

---
|앱 실행 시 | 업무 완료 후 고객 추가 시| 업무 종료 후 초기화 버튼 클릭 시 |
|------|---|---|
|![AppStart](https://github.com/shlim0/ios-bank-manager/assets/142188004/ab2d9a45-95c5-4eb4-9fbe-64753a70a016)|![TaskClearTaskAdd](https://github.com/shlim0/ios-bank-manager/assets/142188004/c33db3aa-b27e-4a99-91ed-18e380092be3)|![TaskClearResetButton](https://github.com/shlim0/ios-bank-manager/assets/142188004/e30cf997-2b13-4aec-8208-6c744f128700)|
|&nbsp;&nbsp;&nbsp;업무 도중 고객 추가 버튼 클릭 시&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;대기 중 화면 스크롤 시&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;업무 도중 초기화 버튼 클릭 시&nbsp;&nbsp;&nbsp;|
|![TaskingAddButtonClick](https://github.com/shlim0/ios-bank-manager/assets/142188004/70d20e76-a195-4511-8f60-10fad7366fc6)|![ScrollView](https://github.com/shlim0/ios-bank-manager/assets/142188004/7151a67e-046a-4984-8539-4785f734aa23)|![ResetButton](https://github.com/shlim0/ios-bank-manager/assets/142188004/e688a4f8-3284-49f3-aac7-ea8ec756fa6b)|


### 트러블 슈팅(추구하고자 했던 방향과 오류 그리고 알게된 점) ⛳️

---
[JaeHyeok & Jjong Trouble Shooting](https://jjong-my.notion.site/Trouble-Shooting-b42d1b0e2d7043f892b009573a38f96b)









