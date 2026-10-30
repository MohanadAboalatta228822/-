<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EGYPT-Ai | منصة تعلم بايثون الفرعونية</title>
    <!-- Brython for Python execution in browser -->
    <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/brython/3.11.0/brython.min.js"></script>
    <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/brython/3.11.0/brython_stdlib.min.js"></script>
    <!-- Fonts & Icons -->
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;900&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        :root {
            --pharaonic-gold: #f3a833;
            --gold-light: #ffd700;
            --gold-dark: #b87b14;
            --lapis-blue: #0b192c;
            --lapis-card: #1e3e62;
            --bg-dark: #070f18;
            --text-light: #f5f5f5;
            --text-muted: #b0c4de;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Cairo', sans-serif;
        }

        body {
            background-color: var(--bg-dark);
            color: var(--text-light);
            background-image: radial-gradient(circle at 50% 10%, rgba(243, 168, 51, 0.08) 0%, transparent 60%);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        header {
            background: linear-gradient(180deg, #0b192c 0%, #070f18 100%);
            border-bottom: 3px solid var(--pharaonic-gold);
            padding: 20px;
            text-align: center;
            box-shadow: 0 4px 20px rgba(243, 168, 51, 0.2);
        }

        .logo-title {
            font-size: 32px;
            font-weight: 900;
            color: var(--pharaonic-gold);
            text-shadow: 0 0 15px rgba(243, 168, 51, 0.4);
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
        }

        .cartouche {
            display: inline-block;
            border: 2px solid var(--pharaonic-gold);
            padding: 6px 20px;
            border-radius: 30px;
            background: rgba(243, 168, 51, 0.1);
            font-size: 14px;
            color: var(--gold-light);
            margin-top: 8px;
            font-weight: bold;
        }

        .container {
            max-width: 1100px;
            margin: 20px auto;
            padding: 0 15px;
            flex: 1;
            width: 100%;
        }

        /* Lesson Card Styling */
        .lesson-card {
            background: var(--lapis-card);
            border: 2px solid rgba(243, 168, 51, 0.3);
            border-radius: 14px;
            padding: 25px;
            margin-bottom: 25px;
            box-shadow: 0 8px 25px rgba(0,0,0,0.4);
            transition: all 0.3s ease;
        }

        .lesson-card:hover {
            border-color: var(--pharaonic-gold);
            box-shadow: 0 10px 30px rgba(243, 168, 51, 0.25);
        }

        .lesson-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px dashed rgba(243, 168, 51, 0.4);
            padding-bottom: 12px;
            margin-bottom: 15px;
        }

        .lesson-title {
            font-size: 20px;
            color: var(--gold-light);
            font-weight: 800;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .lesson-desc {
            color: var(--text-muted);
            font-size: 14px;
            line-height: 1.6;
            margin-bottom: 15px;
        }

        .code-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }

        .editor-box, .output-box {
            background: #050b12;
            border: 1px solid rgba(243, 168, 51, 0.25);
            border-radius: 8px;
            overflow: hidden;
            display: flex;
            flex-direction: column;
        }

        .box-title {
            background: rgba(243, 168, 51, 0.15);
            padding: 8px 12px;
            font-size: 12px;
            font-weight: bold;
            color: var(--pharaonic-gold);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        textarea.code-input {
            width: 100%;
            height: 140px;
            background: transparent;
            color: #50fa7b;
            border: none;
            padding: 10px;
            font-family: 'Courier New', Courier, monospace;
            font-size: 13px;
            resize: none;
            outline: none;
            line-height: 1.4;
        }

        .console-output {
            padding: 10px;
            color: #f8f8f2;
            font-family: 'Courier New', Courier, monospace;
            font-size: 13px;
            height: 140px;
            overflow-y: auto;
            white-space: pre-wrap;
        }

        .run-btn {
            background: linear-gradient(45deg, var(--pharaonic-gold), var(--gold-dark));
            color: #000;
            border: none;
            padding: 4px 12px;
            border-radius: 4px;
            font-weight: bold;
            font-size: 11px;
            cursor: pointer;
        }

        .run-btn:active {
            transform: scale(0.95);
        }

        footer {
            text-align: center;
            padding: 20px;
            background: #0b192c;
            border-top: 2px solid rgba(243, 168, 51, 0.2);
            color: var(--text-muted);
            font-size: 13px;
            margin-top: 30px;
        }

        @media (max-width: 768px) {
            .code-grid { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body onload="brython()">

    <header>
        <div class="logo-title">
            <i class="fa-solid fa-ankh"></i> منصة EGYPT-Ai لتعليم بايثون OOP
        </div>
        <div class="cartouche">
            إعداد المستشار والمدرب: مهند أبوالعطا | تواصل: 01098990142 𓋹
        </div>
    </header>

    <div class="container" id="lessonsContainer">
        <!-- Lessons will load dynamically or statically -->
        
        <!-- Lesson 1 -->
        <div class="lesson-card">
            <div class="lesson-header">
                <div class="lesson-title"><i class="fa-solid fa-scroll"></i> الدرس الأول: مقدمة الكلاسات والكائنات (Class & Object)</div>
            </div>
            <p class="lesson-desc">تعلم كيف تصنع قالباً برمجياً (Class) وكيف تستخرج منه كائنات حية (Objects) بخصائص مختلفة.</p>
            <div class="code-grid">
                <div class="editor-box">
                    <div class="box-title"><span>محرر الكود</span> <button class="run-btn" onclick="runCode('code1', 'out1')">تشغيل ⚡</button></div>
                    <textarea id="code1" class="code-input">class Student:
    def __init__(self, name, score):
        self.name = name
        self.score = score

    def welcome(self):
        return f"أهلاً بك يا {self.name}, درجاتك: {self.score}"

s = Student("محمد", 98)
print(s.welcome())</textarea>
                </div>
                <div class="output-box">
                    <div class="box-title">المخرجات</div>
                    <div id="out1" class="console-output">> اضغط تشغيل لعرض النتيجة...</div>
                </div>
            </div>
        </div>

        <!-- Lesson 2 -->
        <div class="lesson-card">
            <div class="lesson-header">
                <div class="lesson-title"><i class="fa-solid fa-scroll"></i> الدرس الثاني: الكبسلة وحماية البيانات (Encapsulation)</div>
            </div>
            <p class="lesson-desc">كيف تحافظ على سرية بياناتك البرمجية وتمنع تعديلها العشوائي باستخدام الشرطات السفلية (__).</p>
            <div class="code-grid">
                <div class="editor-box">
                    <div class="box-title"><span>محرر الكود</span> <button class="run-btn" onclick="runCode('code2', 'out2')">تشغيل ⚡</button></div>
                    <textarea id="code2" class="code-input">class BankAccount:
    def __init__(self, owner, balance):
        self.owner = owner
        self.__balance = balance  # خاص

    def get_balance(self):
        return self.__balance

acc = BankAccount("مهند", 25000)
print(f"المالك: {acc.owner} | الرصيد: {acc.get_balance()} جنيه")</textarea>
                </div>
                <div class="output-box">
                    <div class="box-title">المخرجات</div>
                    <div id="out2" class="console-output">> اضغط تشغيل لعرض النتيجة...</div>
                </div>
            </div>
        </div>

        <!-- Lesson 3 -->
        <div class="lesson-card">
            <div class="lesson-header">
                <div class="lesson-title"><i class="fa-solid fa-scroll"></i> الدرس الثالث: الوراثة وتوارث الخصائص (Inheritance)</div>
            </div>
            <p class="lesson-desc">كيف يرث الكلاس الابن كافة خصائص ودوال الكلاس الأب لتوفير الوقت ومنع تكرار الأكواد.</p>
            <div class="code-grid">
                <div class="editor-box">
                    <div class="box-title"><span>محرر الكود</span> <button class="run-btn" onclick="runCode('code3', 'out3')">تشغيل ⚡</button></div>
                    <textarea id="code3" class="code-input">class Animal:
    def eat(self):
        return "الكائن يتناول طعامه 🍎"

class Cat(Animal):
    def meow(self):
        return "القطة تقول: ميآو 🐱"

c = Cat()
print(c.eat())
print(c.meow())</textarea>
                </div>
                <div class="output-box">
                    <div class="box-title">المخرجات</div>
                    <div id="out3" class="console-output">> اضغط تشغيل لعرض النتيجة...</div>
                </div>
            </div>
        </div>

        <!-- Lesson 4 -->
        <div class="lesson-card">
            <div class="lesson-header">
                <div class="lesson-title"><i class="fa-solid fa-scroll"></i> الدرس الرابع: تعدد الأشكال (Polymorphism)</div>
            </div>
            <p class="lesson-desc">استدعاء نفس اسم الدالة على كائنات مختلفة لتقوم بسلوكيات متنوعة ومخصصة.</p>
            <div class="code-grid">
                <div class="editor-box">
                    <div class="box-title"><span>محرر الكود</span> <button class="run-btn" onclick="runCode('code4', 'out4')">تشغيل ⚡</button></div>
                    <textarea id="code4" class="code-input">class Dog:
    def sound(self): return "هوهو 🐶"

class Duck:
    def sound(self): return "قوا قوا 🦆"

for obj in [Dog(), Duck()]:
    print(obj.sound())</textarea>
                </div>
                <div class="output-box">
                    <div class="box-title">المخرجات</div>
                    <div id="out4" class="console-output">> اضغط تشغيل لعرض النتيجة...</div>
                </div>
            </div>
        </div>

        <!-- Lesson 5 -->
        <div class="lesson-card">
            <div class="lesson-header">
                <div class="lesson-title"><i class="fa-solid fa-scroll"></i> الدرس الخامس: الدوال السحرية (Magic Methods)</div>
            </div>
            <p class="lesson-desc">التحكم في طريقة طباعة الكلاسات والعمليات الحسابية باستخدام الدوال المزدوجة مثل __str__.</p>
            <div class="code-grid">
                <div class="editor-box">
                    <div class="box-title"><span>محرر الكود</span> <button class="run-btn" onclick="runCode('code5', 'out5')">تشغيل ⚡</button></div>
                    <textarea id="code5" class="code-input">class Book:
    def __init__(self, title):
        self.title = title
    def __str__(self):
        return f"كتاب فرعوني: {self.title}"

b = Book("أسرار الأهرامات البرمجية")
print(b)</textarea>
                </div>
                <div class="output-box">
                    <div class="box-title">المخرجات</div>
                    <div id="out5" class="console-output">> اضغط تشغيل لعرض النتيجة...</div>
                </div>
            </div>
        </div>

        <!-- Lesson 6 -->
        <div class="lesson-card">
            <div class="lesson-header">
                <div class="lesson-title"><i class="fa-solid fa-scroll"></i> الدرس السادس: المزخرفات (Decorators)</div>
            </div>
            <p class="lesson-desc">تغليف الدوال وإضافة سلوكيات ومميزات إضافية عليها بكل سهولة باستخدام العلامة @.</p>
            <div class="code-grid">
                <div class="editor-box">
                    <div class="box-title"><span>محرر الكود</span> <button class="run-btn" onclick="runCode('code6', 'out6')">تشغيل ⚡</button></div>
                    <textarea id="code6" class="code-input">def decorator_func(original):
    def wrapper():
        print("--- بدء التنفيذ ---")
        original()
        print("--- انتهاء التنفيذ ---")
    return wrapper

@decorator_func
def say_hi():
    print("مرحباً بك في عالم بايثون الذكي!")

say_hi()</textarea>
                </div>
                <div class="output-box">
                    <div class="box-title">المخرجات</div>
                    <div id="out6" class="console-output">> اضغط تشغيل لعرض النتيجة...</div>
                </div>
            </div>
        </div>

        <!-- Lesson 7 -->
        <div class="lesson-card">
            <div class="lesson-header">
                <div class="lesson-title"><i class="fa-solid fa-scroll"></i> الدرس السابع: مبادئ SOLID البرمجية</div>
            </div>
            <p class="lesson-desc">قواعد الهندسة البرمجية النظيفة وأهمها مبدأ المسؤولية الفردية (SRP) لتصميم أنظمة قابلة للتطوير.</p>
            <div class="code-grid">
                <div class="editor-box">
                    <div class="box-title"><span>محرر الكود</span> <button class="run-btn" onclick="runCode('code7', 'out7')">تشغيل ⚡</button></div>
                    <textarea id="code7" class="code-input">class Logger:
    def log(self, message):
        print(f"[سجل النظام]: {message}")

l = Logger()
l.log("تم تشغيل النظام البرمجي بنجاح ⚡")</textarea>
                </div>
                <div class="output-box">
                    <div class="box-title">المخرجات</div>
                    <div id="out7" class="console-output">> اضغط تشغيل لعرض النتيجة...</div>
                </div>
            </div>
        </div>

        <!-- Lesson 8 -->
        <div class="lesson-card">
            <div class="lesson-header">
                <div class="lesson-title"><i class="fa-solid fa-scroll"></i> الدرس الثامن: البرمجة غير المتزامنة (Asyncio)</div>
            </div>
            <p class="lesson-desc">إدارة المهام المتوازية وتسريع أداء التطبيقات عبر التعامل مع العمليات المؤجلة بذكاء.</p>
            <div class="code-grid">
                <div class="editor-box">
                    <div class="box-title"><span>محرر الكود</span> <button class="run-btn" onclick="runCode('code8', 'out8')">تشغيل ⚡</button></div>
                    <textarea id="code8" class="code-input">import asyncio

async def main():
    print("جاري الاتصال بقاعدة البيانات...")
    await asyncio.sleep(0.5)
    print("تم الاتصال واستلام البيانات بنجاح! 🚀")

asyncio.run(main())</textarea>
                </div>
                <div class="output-box">
                    <div class="box-title">المخرجات</div>
                    <div id="out8" class="console-output">> اضغط تشغيل لعرض النتيجة...</div>
                </div>
            </div>
        </div>

    </div>

    <footer>
        جميع الحقوق محفوظة © EGYPT-Ai | إعداد المدرب: مهند أبوالعطا
    </footer>

    <!-- Python Execution Engine Script -->
    <script type="text/python" id="pythonScript">
from browser import document, window
import sys

class OutputBuffer:
    def __init__(self, output_elem):
        self.output_elem = output_elem
        self.content = ""
    def write(self, text):
        self.content += text
        self.output_elem.text = self.content
    def flush(self):
        pass

def runCode(code_id, out_id):
    out_elem = document[out_id]
    out_elem.text = ""
    code = document[code_id].value
    
    buf = OutputBuffer(out_elem)
    sys.stdout = buf
    sys.stderr = buf
    
    try:
        exec(code, {})
    except Exception as e:
        out_elem.text += f"\nخطأ في التشغيل: {e}"

window.runCode = runCode
    </script>
</body>
</html>ج# -