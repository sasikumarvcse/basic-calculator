# basic-calculator
# basic calculator for addition ,subtraction ,multiplication ,division purposes.
from kivy.app import App
from kivy.uix.boxlayout import BoxLayout
from kivy.uix.button import Button
from kivy.uix.textinput import TextInput

class CalculatorApp(App):
    def build(self):
        self.expression = ''
        layout = BoxLayout(orientation='vertical')
        self.text_input = TextInput(font_size=200, readonly=True, halign='right', multiline=False)
        layout.add_widget(self.text_input)
        buttons = [
            ['7', '8', '9', '/'],
            ['4', '5', '6', '*'],
            ['1', '2', '3', '-'],
            ['0', '.', '=', '+']
        ]
        for row in buttons:
            button_row = BoxLayout()
            for label in row:
                button = Button(text=label)
                button.bind(on_press=self.button_pressed)
                button_row.add_widget(button)
            layout.add_widget(button_row)
        return layout

    def button_pressed(self, instance):
        label = instance.text
        if label == '=':
            try:
                result = str(eval(self.expression))
                self.text_input.text = result
            except:
                self.text_input.text = 'Error'
            self.expression = ''
        else:
            self.expression += label
            self.text_input.text = self.expression

if __name__ == '__main__':
    CalculatorApp().run()
