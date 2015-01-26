package deposit;
 
import org.eclipse.swt.*;
import org.eclipse.swt.graphics.*;
import org.eclipse.swt.widgets.*;
import org.eclipse.swt.layout.*;
import org.eclipse.swt.events.*;
 
public class main {
        private static Text textProcentnajaStavka;
 
        public static void main(String[] args) {
        // TODO Auto-generated method stub
        Display display = new Display();
        //Создаем окно программы
        Shell shell = new Shell(display);
        shell.setMinimumSize(new Point(450, 350)); //устанавливаем мнимальный размер окна
        shell.pack();
        GridLayout gl_shell = new GridLayout(2, false);//создаем слой таблицы
        gl_shell.verticalSpacing = 10; //устаналиваем расстояние между элементами таблицы по вертикали
        shell.setLayout(gl_shell); //устаналиваем данный слой для приложения
       
        Label labelProcentnajaStavka = new Label(shell, SWT.NONE); // создание заметки ( label)
        labelProcentnajaStavka.setText("Процентная ставка"); // добавление текста в элемент
       
        textProcentnajaStavka = new Text(shell, SWT.BORDER);
        textProcentnajaStavka.setLayoutData(new GridData(SWT.FILL, SWT.CENTER, true, false, 1, 1)); //установка параметров слоя для элемента
       
        Label labelKolichestvoDnej = new Label(shell, SWT.NONE); // создание заметки ( label)
        labelKolichestvoDnej.setText("Количество дней начисления процентов"); // добавление текста в элемент
       
        Spinner spinnerKolichestvoDnej = new Spinner(shell, SWT.BORDER);
        spinnerKolichestvoDnej.setLayoutData(new GridData(SWT.FILL, SWT.CENTER, false, false, 1, 1)); //установка параметров слоя для элемента
        spinnerKolichestvoDnej.setMaximum(10000);
       
        Label labelTipGoda = new Label(shell, SWT.NONE); // создание заметки ( label)
        labelTipGoda.setText("Тип года"); // добавление текста в элемент
       
        Button radioButtonNeVisokosnyjGod = new Button(shell, SWT.RADIO);
        radioButtonNeVisokosnyjGod.setSelection(true);//установка значеня
        radioButtonNeVisokosnyjGod.setText("Невисокосный год"); // добавление текста в элемент
        new Label(shell, SWT.NONE); // создание пустой заметки ( label) - для ровной таблицы
       
        Button buttonRadioVisokosnyjGod = new Button(shell, SWT.RADIO);
        buttonRadioVisokosnyjGod.setText("Високосный год"); // добавление текста в элемент
       
        Label labelPrivlechennyhDenezhnyhSredstv = new Label(shell, SWT.NONE); // создание заметки ( label)
        labelPrivlechennyhDenezhnyhSredstv.setText("Сумма привлеченных денежных средств"); // добавление текста в элемент
       
        Spinner spinnerPrivlechennyhDenezhnyhSredstv = new Spinner(shell, SWT.BORDER);
        spinnerPrivlechennyhDenezhnyhSredstv.setIncrement(1000); //установка шага
        spinnerPrivlechennyhDenezhnyhSredstv.setMaximum(10000000); //установка максимума
        spinnerPrivlechennyhDenezhnyhSredstv.setLayoutData(new GridData(SWT.FILL, SWT.CENTER, false, false, 1, 1)); //установка параметров слоя для элемента
       
        Button buttonRasschetProcentov = new Button(shell, SWT.NONE); //создание кнопки рассчета
        buttonRasschetProcentov.setText("Рассчет процентов"); // добавление текста в элемент
       
        Label labelRasschetProcentov = new Label(shell, SWT.NONE); // создание заметки ( label)
        labelRasschetProcentov.setLayoutData(new GridData(SWT.FILL, SWT.CENTER, false, false, 1, 1)); //установка параметров слоя для элемента
        buttonRasschetProcentov.addMouseListener(new MouseAdapter() { //ожидание события от мыши
                @Override
                public void mouseUp(MouseEvent e) { //обработка снажатия мыши
                        double Sp,I,P=spinnerPrivlechennyhDenezhnyhSredstv.getSelection(); //создание переменных, присваивание их
                        int t=spinnerKolichestvoDnej.getSelection(),K; //создание переменных, присваивание их
                        if(radioButtonNeVisokosnyjGod.getSelection()) // если год не високосный
                        {
                                K=365; //устаналиваем значение K=365
                        }
                        else
                        {
                                K=366; //иначе K=366
                        }
                        try //обработка исключения - пытаемся из текстового поля получить числа
                        {
                                I=Double.parseDouble(textProcentnajaStavka.getText()); // из текстового поля получаем число
                                Sp=P*I*t/(K*100); //считаем итоговое значение
                                labelRasschetProcentov.setText(Double.toString(Sp)+" р."); // добавление текста в элемент
                        }
                        catch(Exception ex) //если случилось исключение - то есть в текстовом поле нет числа или есть иные символы
                        {
                                labelRasschetProcentov.setText("Некорректный ввод проц. ставки"); // выводим на экран текст ошибки
                        }
                        }
        });
        shell.open(); //открытие приложения
        while (!shell.isDisposed()) { // цикл до закрытия программы
                if (!display.readAndDispatch()) {
                        display.sleep();
                 }
                }
                //Ресурсы операционной системы
                //должны быть освобождены
                display.dispose();
       
        }
 
}
