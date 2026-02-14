# SBDL Project - Environment Setup Guide

This project requires:

- Python 3.10
- PySpark 3.3.0
- Java 11
- No global Spark 4 leakage

Your machine default setup:
- Python 3.14
- Spark 4
- Java 21

This project runs in its own isolated environment.

---

# Recommended Way to Run the Project (Safe Method)

Always run commands using the wrapper:

```
./run_sbdl.sh <command>
```

Examples:

```
./run_sbdl.sh pytest -q
./run_sbdl.sh python sbdl_main.py local 2022-08-02
```

The wrapper automatically:
- Forces Java 11
- Unsets SPARK_HOME
- Unsets PYSPARK_SUBMIT_ARGS
- Uses pipenv (Python 3.10 + PySpark 3.3.0)

This is the safest method.

---

# Manual Method (Interactive Development Mode)

Use this if you want to work interactively inside the virtual environment.

## 1. Enter project directory

```
cd ~/projects/SBDL
```

## 2. Activate pipenv environment

```
pipenv shell
```

Your prompt should change to:

```
(SBDL) ...
```

Check Python version:

```
python --version
```

It must show:

```
Python 3.10.19
```

---

## 3. Configure Java and Spark variables (Important)

Inside pipenv shell, run:

```
export JAVA_HOME=/opt/homebrew/opt/openjdk@11/libexec/openjdk.jdk/Contents/Home
export PATH="$JAVA_HOME/bin:$PATH"
unset SPARK_HOME
unset PYSPARK_SUBMIT_ARGS
```

This ensures:
- Java 11 is used
- Spark 4 is not used
- PySpark 3.3.0 works correctly

---

## 4. Run tests

```
pytest -q
```

Expected output:

```
1 passed
```

---

## Exit Virtual Environment

To exit:

```
exit
```

---

# Quick Decision Guide

If you want:

Quick execution → use wrapper  

```
./run_sbdl.sh <command>
```

Interactive development → use:

```
pipenv shell
```

Then configure Java and unset Spark variables.

---

# Important Notes

This setup is isolated to this project only.

Other projects can still use:
- Spark 4
- Java 21
- Python 3.14

Nothing global was changed.

---

You are now fully ready to work on the SBDL Spark project safely.