epiPALEOMIX-->epiomix-->epimakefile

```
__init__.py 
该文件的作用就是相当于把自身整个文件夹当作一个包来管理，每当有外部import的时候，就会自动执行里面的函数
```

epicreatemkfile.py，重点关注main函数

```
def main(argv):		# argv是一个list[]
    timestamp = datetime.datetime.now().isoformat()    # 添加时间戳
    try:
        if argv[0].lower() == 'simple':		# 取列表中第一个元素
            template = _TEMPLATE_EPIPALEOMIX_SIMPLE % (timestamp,)		
            print(template, file=sys.stdout)
            return 0
    except IndexError:		# 如果出现IndexError参数错误，则跳过，执行正常的命令
        pass
    template = _TEMPLATE_EPIPALEOMIX % (timestamp,)
    print(template, file=sys.stdout)		# 将结果传入file中
    return 0


if __name__ == "__main__":
    sys.exit(main(sys.argv[1:]))
```

时间戳函数

```
datetime 第一个datetime是包
datetime 第二个datetime是函数
now() 现在的时间
isoformat() 时间格式，command + 点击查看功能
```

epivalidmkfile.py

vaild脚本用于校验mkfile文件

```
import string
from pypeline.common.makefile import \		# 从pypeline等脚本引入某些函数
    read_makefile, \
    IsUnsignedInt, \
    IsFloat, \		# 点击可以查看每个函数的功能
    IsStr, \
    IsBoolean, \
    And, \
    Or, \
    ValueIn, \
    IsNone, \
    StringIn, \
    ValueGE, \
    ValuesSubsetOf, \
    IsListOf

EXCLUDEBED = Or(IsListOf(IsStr), IsStr, IsNone, default=None)

def _alphanum_check(whitelist):		# check字母和数字
    description = "characters a-z, A-Z, 0-9%s allowed"
    description %= (", and %r" % whitelist,) if whitelist else ""

    whitelist += string.ascii_letters + string.digits

    return And(IsStr(),
               ValuesSubsetOf(whitelist, description=description))



_VALID_BED_NAME = _VALID_TARGET_NAME = \
    And(_alphanum_check(whitelist=".-"),
        ValueGE(2, key=len, description="at least two characters long"))

_VALIDATION_OPTIONS = {
    "BamPath": IsStr,
    "--MinMappingQuality": IsUnsignedInt(default=25),
    "--MinAlignmentLength": IsUnsignedInt(default=25),
    "--NoReadsChecked": IsUnsignedInt(default=5000)
}

_VALIDATION_GCCORRECT = {
    "Enabled": IsBoolean(default=False),
    "--NoRegions": Or(IsUnsignedInt, IsStr, default=200), 
    "--ChromUsed": Or(IsStr,IsUnsignedInt, default="all"),   ## the is new
    "--MappaUniqueness": IsFloat(default=0.9)
}



_VALIDATION_NUCLEO = {
    "Enabled": IsBoolean(default=False),
    "Apply_GC_Correction": IsBoolean(default=True),
    "ExcludeBed": EXCLUDEBED,
    "--NucleosomeFlanks": IsUnsignedInt(default=25),
    "--NucleosomeSize": IsUnsignedInt(default=147),
    "--NucleosomeOffset": IsUnsignedInt(default=12)
}
_VALIDATION_METHYL = {
    "Enabled": IsBoolean(default=False),
    "ExcludeBed": EXCLUDEBED,
    "--ReadBases": IsUnsignedInt(default=15),
    "--MinBaseQuality": IsUnsignedInt(default=20),
    "--SkipThreePrime": IsUnsignedInt(default=0),
    "--SkipFivePrime": IsUnsignedInt(default=0),
    "--Primes": StringIn(('five', 'three','both'), default='five')
}
_VALIDATION_PHASO = {
    "Enabled": IsBoolean(default=False),
    "ExcludeBed": EXCLUDEBED,
    "Apply_GC_Correction": IsBoolean(default=False),
    "--SubsetPileup": IsUnsignedInt(default=1),
    "--MaxRange": IsUnsignedInt(default=1500)
}
_VALIDATION_WRITEDEPTH = {
    "Enabled": IsBoolean(default=False),
    "ExcludeBed": EXCLUDEBED,
    "Apply_GC_Correction": IsBoolean(default=True)
}

_VALIDATION_TOOLS = {
    "BamInfo": _VALIDATION_OPTIONS,
    "GCcorrect": _VALIDATION_GCCORRECT,
    "NucleoMap": _VALIDATION_NUCLEO,
    "MethylMap": _VALIDATION_METHYL,
    "Phasogram": _VALIDATION_PHASO,
    "WriteDepth": _VALIDATION_WRITEDEPTH
}
# _VALIDATION_BED = {
#     "Path": IsStr
#     # "MakeMergePlot": IsBoolean(default=False)
# }

_VALIDATION = {
    "BamInputs": {  # BAMFILES:
        _VALID_TARGET_NAME: _VALIDATION_TOOLS
    },
    "Prefixes": {
        "--FastaPath": IsStr,
        "--MappabilityPath": Or(IsStr, IsNone)
    },
    "BedFiles": {
        'MappabilityFilter': IsBoolean(default=False),
        'MappabilityScore': IsFloat(default=0.9),
        _VALID_BED_NAME: IsStr
        ## _VALID_BED_NAME: _VALIDATION_BED
    }
}


def read_epiomix_makefile(argv):		# 查找makefile
    for f in argv:
        if isinstance(f, str) and f.endswith('.yaml'):
            yield read_makefile(f, _VALIDATION)

```

1. yeild和return的区别

共同点：**return**和**yield**都用来返回值；在一次性地返回所有值场景**中return**和**yield**的作用是一样的。 不同点：如果要返回的数据是通过for等循环生成的迭代器类型数据（如列表、元组），**return**只能在循环外部一次性地返回，yeild则可以在循环内部逐个元素返回。

2. raise()，是python的内置函数。在pycharm中，紫色和红色表示python的内置函数，绿色则为自定义函数。

用raise语句来引发一个异常。异常/错误对象必须有一个名字，且它们应是Error或Exception类的子类。

3. python的回调函数

回调函数就是一个通过函数名调用的函数。如果你把函数的名字（地址）作为参数传递给另一个函数，当这个参数被用来调用其所指向的函数时，我们就说这是回调函数。回调函数不是由该函数的实现方直接调用，而是在特定的事件或条件发生时由另外的一方调用的，用于对该事件或条件进行响应。

4. python脚本中会出现大量的继承，需要理解并学会使用。