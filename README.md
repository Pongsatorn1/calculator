# calculator
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace WindowsFormsApplication2
{
    public partial class Form1 : Form
    {
        double value = 0; //ประตัวแปล value เท่ากับ 0
        string operation = "";// ประกาศ operation เป็นข้อความ
        bool operation_pressed = false; //ประกาศบูลีน

        public Form1()
        {
            InitializeComponent();
        }

    
        private void button_Click(object sender, EventArgs e) //ตั้ง event รับค่าตัวเลขเข้ามาจากปุ่ม botton 
        {
            if ((result.Text == "0") || (operation_pressed)) //เมื่อกดรับค่าจากปุ่ม botton มาแล้วให้ล้างค่าเลข 0 ที่เป็นข้อความออก
                result.Clear();

            operation_pressed = false; //โค๊ตในส่วนนี้จะเป็นดักจุดทศนิยม ห้ามใส่เกิน 1 จุด
            Button b = (Button)sender;
            if (b.Text == ".")
            {
                if(!result.Text.Contains(".")) //นำข้อความที่ได้จาก textbox บวกด้วยกับค่าที่จากปุ่ม botton
                    result.Text = result.Text + b.Text;
            }
            else

            result.Text = result.Text + b.Text; //ถ้าอยู่นอกรณีก็ให้ นำข้อความที่ได้จาก textbox บวกด้วยกับค่าที่จากปุ่ม botton
        }

        private void button5_Click(object sender, EventArgs e)
        {
            result.Text = "0";  //ปุ่ม CE  เอาไว้ล้างค่าที่พึงพิมเอาไว้ แล้วเพิ่มเลข 0 เข้าไปไป
        
        }

        private void operator_click(object sender, EventArgs e) //เอาไว้รับค่า operator ที่คลิกเข้าไป
        {
            Button b = (Button)sender;

            if (value != 0) //ถ้า value ไม่เท่ากับ 0
            {
                equal.PerformClick(); //เมื่อกดตัวเลขและตามด้วย oparetor เสร็จ ให้คลิกปุ่ม botton ที่เป็นเครื่องหมายเทากับ
                operation_pressed = true; //operation_pressed เป็นจริง
                operation = b.Text;  // operation เป็็นค่าที่ได้จากปุ่ม botton
                equation.Text = value + " " + operation; //ค่าที่แสดงตรงประวัตินั้นเป็นค่าทำการบวกลบตัวเลขเสร็จแล้วไปโชว์ตามด้วยเครื่องหมาย oparetor
            }
            else
            { 
            operation = b.Text;
            value = Double.Parse(result.Text);
            operation_pressed = true;//operation_pressed เป็นจริง
            equation.Text = value + " " + operation;//ค่าที่แสดงตรงประวัตินั้นเป็นค่าทำการบวกลบตัวเลขเสร็จแล้วไปโชว์ตามด้วยเครื่องหมาย oparetor
            }
        }

        private void button11_Click(object sender, EventArgs e)
        {
            op(); //เรียกใช้ Medthod ชื่อ op
        }
        public void op()
        {
            equation.Text = ""; //ให้แสดงเครื่องหมาย operator ในประวัติ 
            switch (operation) //switch case (operation)
            {

                case "+":
                    result.Text = (value + Double.Parse(result.Text)).ToString(); //แปลงค่าจาก textbox ให้เป็นตัวเลขแล้วนำไปบวก ค่าใน value แล้วแปลงค่าเป็นข้อความแล้วส่งออกไปแสดงใน Textbox
                    break;
                case "-":
                    result.Text = (value - Double.Parse(result.Text)).ToString();//แปลงค่าจาก textbox ให้เป็นตัวเลขแล้วนำไปลบ ค่าใน value แล้วแปลงค่าเป็นข้อความแล้วส่งออกไปแสดงใน Textbox
                    break;
                case "*":
                    result.Text = (value * Double.Parse(result.Text)).ToString();//แปลงค่าจาก textbox ให้เป็นตัวเลขแล้วนำไปคูณ ค่าใน value แล้วแปลงค่าเป็นข้อความแล้วส่งออกไปแสดงใน Textbox
                    break;
                case "/":
                    result.Text = (value / Double.Parse(result.Text)).ToString();//แปลงค่าจาก textbox ให้เป็นตัวเลขแล้วนำไปหาร ค่าใน value แล้วแปลงค่าเป็นข้อความแล้วส่งออกไปแสดงใน Textbox
                    break;
                default:
                    break;
            }//End switch
            value = Int32.Parse(result.Text); //แปลงค่าจาก textbox ให้เป็นตัวเลข ในตัวแปล value
            operation = ""; //เครื่องหมาย oprator
        }
        private void button6_Click(object sender, EventArgs e)
        {
            result.Text = "0"; //ล่างค่าในtextbox
            value = 0; //ประกาศ valueเ เท่ากับ 0 
            equation.Text = " ";  //ล้างประวัติทั้งหมด
        }

        private void result_TextChanged(object sender, EventArgs e)
        {

        }

        private void Form1_Load(object sender, EventArgs e)
        {

        }

        private void Form1_KeyPress(object sender, KeyPressEventArgs e)
        {
            switch (e.KeyChar.ToString()) //สามรารถรับค่าจาก คีร์บอร์ด
            {
                case "0":
                    zero.PerformClick(); //กดเลข 0 ให้กดปุ่ม botton zero
                    break;

                case "1":
                    one.PerformClick();//กดเลข 1 ให้กดปุ่ม botton one
                    break;

                case "2":
                    two.PerformClick();//กดเลข 2 ให้กดปุ่ม botton two
                    break;

                case "3":
                    three.PerformClick();//กดเลข 3 ให้กดปุ่ม botton three
                    break;

                case "4":
                    four.PerformClick();//กดเลข 4 ให้กดปุ่ม botton four
                    break;

                case "5":
                    five.PerformClick();//กดเลข 5 ให้กดปุ่ม botton five
                    break;

                case "6":
                    six.PerformClick();//กดเลข 6 ให้กดปุ่ม botton six
                    break;

                case "7":
                    seven.PerformClick();//กดเลข 7 ให้กดปุ่ม botton seven
                    break;

                case "8":
                    egg.PerformClick();//กดเลข 8 ให้กดปุ่ม botton egg
                    break;

                case "9":
                    nigth.PerformClick();//กดเลข 9 ให้กดปุ่ม botton nigth
                    break;

                case "/":
                    div.PerformClick();//กด / ให้กดปุ่ม botton div
                    break;

                case "*":
                    times.PerformClick();//กด * ให้กดปุ่ม botton times
                    break;

                case "-":
                    sub.PerformClick();//กด - ให้กดปุ่ม botton sub
                    break;

                case "+":
                    add.PerformClick();//กด + ให้กดปุ่ม botton add
                    break;

                case "=":
                    equal.PerformClick();//กด = ให้กดปุ่ม botton equal
                    break;


                case "ENTER":
                    equal.PerformClick();//กด ENTER ให้กดปุ่ม botton equal

                    break;
                default:
                    break;



            }
            equal.Focus(); //เป็นการให้มัน โฟกัสี่ปุ่ม ENTER เป็นพิเศษ
        }
    }
}
