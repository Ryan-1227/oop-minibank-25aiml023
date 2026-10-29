
**MiniBank** is an enterprise-grade, console-based banking application developed progressively across 14 laboratory sessions. It demonstrates core and advanced Object-Oriented Programming (OOP) paradigms in modern Java (JDK 17+), integrating:

- **Encapsulated Data Models & Records** (`BankInfo`, `Customer`, `Account`, `Command`)
- **Polymorphism & Class Hierarchies** (`SavingsAccount`, `CurrentAccount`, `FixedDepositAccount`)
- **Interfaces & Lambdas** (`Transactable`, `InterestBearing`, `WithdrawRule`, `Premium`)
- **Custom Metadata & Runtime Reflection** (`@Id`, `@Positive`, `@MaxLength`, `@Audit`, `AnnotationValidator`)
- **Robust Exception Hierarchies** (`BankException`, `InsufficientFundsException` with shortfall tracking)
- **Multi-threading & Thread Safety** (Race condition prevention via `synchronized` methods, `AccountWorker`)
- **Enterprise Concurrency Engine** (`TransactionProcessor`, `ExecutorService`, Deadlock Prevention via consistent lock ordering, Producer-Consumer buffer with `wait()` / `notify()`)
- **Object Serialization & NIO Log Processing** (`StatePersister`, `TransactionLog`, `ReportGenerator` with `DirectoryStream`)
- **Collections Framework & Sorting** (`HashMap`, `ArrayList`, `Comparator`, `Comparable`, `ConcurrentHashMap`)
- **Generic Data Access Layer** (`Repository<T>` with reflected `@Id` resolution, `@SafeVarargs`, bounded generic parameters `<N extends Number>`)
- **Layered Architecture & Comprehensive JUnit 5 Test Suite** (`BankService`, `MiniBankTest`)

---

## 🚀 How to Build and Run

### Prerequisites
- **Java Development Kit (JDK 17 or higher)** (`javac` and `java` available in PATH).
- **Git** for version control.

### Option 1: Using Automation Scripts (Recommended)

#### On macOS / Linux:
```bash
# 1. Build and package minibank.jar
./build.sh

# 2. Run the interactive MiniBank application
./run.sh

# 3. Run all JUnit 5 unit tests
./test.sh
```

#### On Windows:
```cmd
:: 1. Build and package minibank.jar
build.bat

:: 2. Run the interactive MiniBank application
run.bat

:: 3. Run all JUnit 5 unit tests
test.bat
```

### Option 2: Using Standard JDK Command Line

#### 1. Compile the Source Code:
```bash
mkdir -p bin
javac -d bin $(find src -name "*.java")
```

#### 2. Package the Runnable JAR:
```bash
jar --create --file minibank.jar --main-class minibank.MiniBank -C bin .
```

#### 3. Run the Application:
```bash
java -jar minibank.jar
```

#### 4. Run the JUnit 5 Test Suite:
```bash
mkdir -p bin-test
javac -cp "bin:lib/junit-platform-console-standalone.jar" -d bin-test $(find test -name "*.java")
java -jar lib/junit-platform-console-standalone.jar execute -cp "bin:bin-test" --select-class minibank.MiniBankTest
```

---

## 🧭 Console Menu

The interactive application deliberately presents nine options only. Options 1–8 provide
the account operations and batch-processing demonstration; option 9 saves the current
state and exits. The automated checks are run with `test.bat` or `test.sh`, rather than
from the application menu.

---

---
