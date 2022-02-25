pytest

-s：用于关闭捕捉（不向测试报告输送测试结果），从而输出打印信息

-v：用于显示具体的信息

-k：运行用例名称中包含某特定字符串的用例

```python
pytest.main(['-k','kkk'])
```

-q：简化输出信息

-x：如果出现一条失败的用例，立刻终止



指定目录以及特定的方法执行:

```python
pytest.main([''-s,'./testing/test_111.py::test_222'])
```



生成测试报告：

```python 
pytest.main(['--junit-xml=./report/junit_report01.xml'])
```



通过标记表达式运行

pytest.ini

```ini
[pytest]
markers =  
	slow: marks tests as slow
	smoke
	Regression: Remark
```

```python
@pytest.mark.slow
def test_01():
   pass
    
def __name__ = "__main__":
    pytest.main(['-m', 'slow'])
```



多进程运行用例：
安装插件：pip install pytest-xdist

```python
pytest.main(['-n','2','test_many.py'])
```

数量不能超过cpu的核心数

失败重跑

安装插件：pip install pytest-rerunfailures

```python
pytest.main(['--reruns','3','test_rerun.py'])
```

