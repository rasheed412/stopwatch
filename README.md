from PyQt5 import QtWidgets, uic
from PyQt5.QtWidgets import QMessageBox
from PyQt5 import QtCore
import sys
 
class Example(QtWidgets.QMainWindow):
    def __init__(self):
        super(Example, self).__init__()
        uic.loadUi('window.ui', self)

        self.timer = QtCore.QTimer()
        self.time = QtCore.QTime(0, 0, 0)
        self.timer.timeout.connect(self.timerEvent)

        self.pushButtonStart.clicked.connect(self.onStart)
        self.pushButtonStop.clicked.connect(self.onStop)
        self.pushButtonReset.clicked.connect(self.onReset)

    def timerEvent(self):
        self.time = self.time.addSecs(1)
        self.timeEdit.setTime(self.time)

    def onStart(self):
        print('start')
        self.timer.start(100)

    def onStop(self):
        print('stop')
        self.timer.stop()

    def onReset(self):
        self.time = QtCore.QTime(0, 0, 0)
        self.timeEdit.setTime(self.time)

app = QtWidgets.QApplication([])
win = Example()
win.show()
sys.exit(app.exec())
