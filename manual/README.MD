# 🧾 Manual for `.blahjz` File Configuration in Blahzlow

Blahzlow supports automated test execution by reading structured `.blahjz` model files that define **workflow test cases**. These files are written in JSON format and serve as instructions for the boardtest engine.


## 📁 What is a `.blahjz` file?

A `.blahjz` file is a **test configuration file** used to describe:
- The script to be tested
- The method calls
- The expected values
- Step ordering
- A test description for documentation

---

## 📐 File Structure Overview

Here is an example of a valid `.blahjz` test model entry:

```json
{
  "NAME": "pyx_test_route_v0_x01_txt",
  "FILE": "pyx_test_route.py",
  "STEP": "0",
  "MV": "write('hello world');app_lst(1);WriteFile('stream_writer_test.txt','success_x_0:01:x');app_lst_err(-1)",
  "VAL": ["hello world", 1, "stream_writer_test.txt", "success_x_0:01:x", -1],
  "DESC": "ROADMAP TO TEST pyx_test_route.py V0x1A:0x00"
}
````

---

## 🧩 Description of Fields

| Field    | Description                                                                                                                      |
| -------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `"NAME"` | The name or identifier of the test step. Use a clear, unique name for each step.                                                 |
| `"FILE"` | The Python source file that will be tested. Use a relative or absolute path.                                                     |
| `"STEP"` | The execution order or index. `"0"` runs first, `"1"` runs second, etc.                                                          |
| `"MV"`   | A **string of method calls** with their parameters, written in Python-style syntax. Separate multiple calls with semicolons `;`. |
| `"VAL"`  | A **list** of the expected values for each method. Each value corresponds to its call in `"MV"`.                                 |
| `"DESC"` | A human-readable string describing what the step is testing. Great for debugging or documentation.                               |

---

## 🛠️ Writing a .blahjz File Manually

To create a `.blahjz` file manually, simply paste your model into a file:

```json
{
  "NAME": "pyx_test_route_v0_x01_txt",
  "FILE": "pyx_test_route.py",
  "STEP": "0",
  "MV": "write('hello world');app_lst(1);WriteFile('stream_writer_test.txt','success_x_0:01:x');app_lst_err(-1)",
  "VAL": ["hello world", 1, "stream_writer_test.txt", "success_x_0:01:x", -1],
  "DESC": "ROADMAP TO TEST pyx_test_route.py V0x1A:0x00"
}
```

Save it with a `.blahjz` extension, for example:

```
models/blahjz_file_model_0x.blahjz
```

---

## ⚙️ Using a .blahjz Model in Blahzlow

Once your model file is created, you can configure Blahzlow to load it using the function:

```python
set_config_model("models/blahjz_file_model_0x.blahjz")
```

This will register the workflow into the Blahzlow test engine and allow you to execute it using:

```python
set_exec_bat()
```

---

## 🧠 Notes

* The `"MV"` and `"VAL"` fields must match in logical order.
* The method calls in `"MV"` must exist and be callable in the target `"FILE"`.
* Always use `;` between multiple function calls inside `"MV"`.

---

## ✅ Example Summary

Here’s a simplified overview for clarity:

```python
# Load test model configuration
set_config_model("models/blahjz_file_model_0x.blahjz")

# Prepare bat file for execution
set_write_exec()

# Execute boardtest flow
set_exec_bat()

# View result (optionally)
get_result_viewer("result_output_path.txt", type="WEBVIEW")
```

---

## 📬 Need Help?

Email the author at [eussmool@gmail.com](mailto:eussmool@gmail.com) or visit the repository:
🔗 [https://github.com/ssmool/blahzlow](https://github.com/ssmool/blahzlow)



