# remembrance
v1.0
from PyQt5.QtCore import Qt
from PyQt5.QtWidgets import QApplication, QWidget, QPushButton, QLabel, QVBoxLayout, QMessageBox, QRadioButton, QHBoxLayout, QGroupBox, QButtonGroup
from random import shuffle, randint
class Question():
    def __init__(
        self, question, right_answer, wrong1, wrong2, wrong3,
    ):
        self.question = question
        self.right_answer = right_answer
        self.wrong1 = wrong1
        self.wrong2 = wrong2
        self.wrong3 = wrong3
  * crystal_sage%69*
question_list = []
question_list.append(Question('Государственный язык Бразилии', 'Португ', 'Англий', 'Испан', 'Бразил'))
question_list.append(Question('Какого цвета нет на флаге России?', 'Зелёный', 'Красный', 'Белый', 'Синий'))
question_list.append(Question('Национальная хижина якунтов', 'Ураса', 'Юрта', 'Иглу', 'Хата'))
question_list.append(Question('Сколько букв в слове ёж?', '12', '21', '2', '8'))
question_list.append(Question('Во сколько заканчиваются занятия?', '15:30', 'никогда', 'что?', 'алё'))
question_list.append(Question('Какой эьто вопрос?', 'незнаю', 'a', 'в слове это ошибка', ','))

app = QApplication([])
main_win = QWidget()
main_win.resize(600, 300)
main_win.setWindowTitle('Memory card')

lb_question = QLabel('Какой национальности не существует?')
knopka = QPushButton('Ответить')
RadioGroupBox = QGroupBox("Варианты ответов")
rbtn_1 = QRadioButton('Энцы')
rbtn_2 = QRadioButton('Смурфы')
rbtn_3 = QRadioButton('Чулымцы')
rbtn_4 = QRadioButton('Алеуты')
answers = [rbtn_1, rbtn_2, rbtn_3, rbtn_4]
RadioGroup = QButtonGroup()
RadioGroup.addButton(rbtn_1)
RadioGroup.addButton(rbtn_2)
RadioGroup.addButton(rbtn_3)
RadioGroup.addButton(rbtn_4)
layout_ans1 = QHBoxLayout()
layout_ans2 = QVBoxLayout()
layout_ans3 = QVBoxLayout()
layout_ans2.addWidget(rbtn_1)
layout_ans2.addWidget(rbtn_2)
layout_ans3.addWidget(rbtn_3)
layout_ans3.addWidget(rbtn_4)
layout_ans1.addLayout(layout_ans2)
layout_ans1.addLayout(layout_ans3)
RadioGroupBox.setLayout(layout_ans1)
AnsGroupBox = QGroupBox("Результат теста")
lb_Result = QLabel('прав ты или нет?')
lb_Correct = QLabel('ответ будет тут!')
layout_res = QVBoxLayout()
layout_res.addWidget(lb_Result, alignment=(Qt.AlignLeft | Qt.AlignTop))
layout_res.addWidget(lb_Correct, alignment=Qt.AlignHCenter, stretch=2)
AnsGroupBox.setLayout(layout_res)
layout_line1 = QHBoxLayout()
layout_line2 = QHBoxLayout()
layout_line3 = QHBoxLayout()
layout_line1.addWidget(lb_question, alignment=(Qt.AlignHCenter | Qt.AlignVCenter))
layout_line2.addWidget(RadioGroupBox)
layout_line2.addWidget(AnsGroupBox)
AnsGroupBox.hide()
def check_answer():
    if answers[0].isChecked():
        show_correct('Правильно!')
        main_win.score += 1
        print('Статистика\n-Всего вопросов: ', main_win.total, '\n-Правильных ответов:', main_win.score)
        print('Рейтинг:', (main_win.score/main_win.total*100), '%')
    else:
        if answers[1].isChecked() or answers[2].isChecked() or answers[3].isChecked():
            show_correct('Неверно!')
            print('Рейтинг:', (main_win.score/main_win.total*100), '%')
def show_correct(res):
    '''показать результат - установим переданный текст в надпись "результат" и покажем нужную панель '''
    lb_Result.setText(res)
    show_result()
def test():
    ''' временная функция, которая позволяет нажатием на кнопку вызывать по очереди
    show_result() либо show_question()'''
    if 'Ответить' == knopka.text():
        show_result()
    else:
        show_question()
layout_line3.addStretch(1)
layout_line3.addWidget(knopka, stretch=2)
layout_line3.addStretch(1)
layout_card = QVBoxLayout()
layout_card.addLayout(layout_line1, stretch=2) 
layout_card.addLayout(layout_line2, stretch=8)
layout_card.addStretch(1)
layout_card.addLayout(layout_line3, stretch=1)
layout_card.addStretch(1)
layout_card.setSpacing(5)
def show_result():
    "показать панель ответов"
    RadioGroupBox.hide()
    AnsGroupBox.show()
    knopka.setText('Следующий вопрос')
def show_question():
    "показать панель вопросов"
    RadioGroupBox.show()
    AnsGroupBox.hide()
    knopka.setText('Ответить')
    RadioGroup.setExclusive(False)
    rbtn_1.setChecked(False)
    rbtn_2.setChecked(False)
    rbtn_3.setChecked(False)
    rbtn_4.setChecked(False)
    RadioGroup.setExclusive(True)

def ask(q: Question):
    shuffle(answers)
    answers[0].setText(q.right_answer)
    answers[1].setText(q.wrong1)
    answers[2].setText(q.wrong2)
    answers[3].setText(q.wrong3)

    lb_question.setText(q.question)
    lb_Correct.setText(q.right_answer)
    show_question()
def next_question():
    main_win.total += 1
    print('Статистика\n-ВВопросов:', main_win, '\n-Правильных ответов:', main_win.score)
    cur_question = randint(0, len(question_list) - 1)
    q = question_list[cur_question]
    ask(q)
def click_OK():
    if knopka.text() == 'Ответить':
        check_answer() 
    else:
        next_question()
main_win.setLayout(layout_card)

shuffle(answers)
q = Question('Государственный язык Бразилии', 'Потруг', 'Бразил', 'Испан', 'Bnfk')
ask(q)
knopka.clicked.connect(click_OK)
main_win.score = 0
main_win.total = 0
next_question()
main_win.show()
app.exec_()
