## STM32 side library

### Library 

PS4_serial, PS4_command

### Testing

PC_serial, main.cpp, pin_define.h


## The only thing to do is to modify this part

~~~
    void    high_func_CommandChange(){}
    void    high_func_LH(){}
    void    high_func_RH(){}
    void    high_func_L2(){}
    void    high_func_R2(){}
    void    high_func_TRI(){}
    void    high_func_CIR(){}
    void    high_func_CRO(){}
    void    high_func_SQU(){}
    void    high_func_UP()
            {
                char a[5] = {'h','i','g','h',' '};
                PC_send(a,5);
            }
    void    high_func_RIGHT(){}
    void    high_func_DOWN(){}
    void    high_func_LEFT(){}
    void    high_func_L1(){}
    void    high_func_L3(){}
    void    high_func_R1(){}
    void    high_func_R3(){}
    void    high_func_SHARE(){}
    void    high_func_OPTIONS(){}
    
    
    void    low_func_CommandChange(){}
    void    low_func_LH(){}
    void    low_func_RH(){}
    void    low_func_L2(){}
    void    low_func_R2(){}
    void    low_func_TRI(){}
    void    low_func_CIR(){}
    void    low_func_CRO(){}
    void    low_func_SQU(){}
    void    low_func_UP()
            {
                char a[5] = {'l','o','w',' ',' '};
                PC_send(a,5);
            }
    void    low_func_RIGHT(){}
    void    low_func_DOWN(){}
    void    low_func_LEFT(){}
    void    low_func_L1(){}
    void    low_func_L3(){}
    void    low_func_R1(){}
    void    low_func_R3(){}
    void    low_func_SHARE(){}
    void    low_func_OPTIONS(){}
    
    
    void    fall_func_CommandChange(){}
    void    fall_func_LH(){}
    void    fall_func_RH(){}
    void    fall_func_L2(){}
    void    fall_func_R2(){}
    void    fall_func_TRI(){}
    void    fall_func_CIR(){}
    void    fall_func_CRO(){}
    void    fall_func_SQU(){}
    void    fall_func_UP(){
                char a[5] = {'f','a','l','l',' '};
                PC_send(a,5);
            }
    void    fall_func_RIGHT(){}
    void    fall_func_DOWN(){}
    void    fall_func_LEFT(){}
    void    fall_func_L1(){}
    void    fall_func_L3(){}
    void    fall_func_R1(){}
    void    fall_func_R3(){}
    void    fall_func_SHARE(){}
    void    fall_func_OPTIONS(){}
    
    
    void    rise_func_CommandChange(){}
    void    rise_func_LH(){}
    void    rise_func_RH(){}
    void    rise_func_L2(){}
    void    rise_func_R2(){}
    void    rise_func_TRI(){}
    void    rise_func_CIR(){}
    void    rise_func_CRO(){}
    void    rise_func_SQU(){}
    void    rise_func_UP(){
                char a[5] = {'r','i','s','e',' '};
                PC_send(a,5);
            }
    void    rise_func_RIGHT(){}
    void    rise_func_DOWN(){}
    void    rise_func_LEFT(){}
    void    rise_func_L1(){}
    void    rise_func_L3(){}
    void    rise_func_R1(){}
    void    rise_func_R3(){}
    void    rise_func_SHARE(){}
    void    rise_func_OPTIONS(){}
~~~

## In crimson, we implement these functions in main.cpp

~~~
void high_func_LH()
{
    if (!autoMode)
    {
        if (((joy_range_mid - joy_range) < getLY()) and (getLY() < (joy_range_mid + joy_range)))
        {
            vt = 0;
        }
        else
        {
            //vt = map(getLY(),0,255,-1,1) * linear_speed ;
            float temp = map(getLY(), 0, 255, -1, 1);
            if (temp < 0)
            {
                vt = (temp * temp) * -1 * linear_speed;
            }
            else
            {
                vt = (temp * temp) * linear_speed;
            }
        }

        if (((joy_range_mid - joy_range) < getLX()) and (getLX() < (joy_range_mid + joy_range)))
        {
            vnt = 0;
        }
        else
        {
            //vnt = map(getLX(),0,255,-1,1) * linear_speed ;
            float temp = map(getLX(), 0, 255, -1, 1);
            if (temp < 0)
            {
                vnt = (temp * temp) * -1 * linear_speed;
            }
            else
            {
                vnt = (temp * temp) * linear_speed;
            }
        }
    }
}
void high_func_RH()
{
    if (!autoMode)
    {
        if (((joy_range_mid - joy_range) < getRX()) and (getRX() < (joy_range_mid + joy_range)))
        {
            wt = 0;
        }
        else
        {
            //wt = map(getRX(),0,255,-1,1) * angular_speed ;
            float temp = map(getRX(), 0, 255, -1, 1);
            if (temp < 0)
            {
                wt = (temp * temp) * -1 * angular_speed;
            }
            else
            {
                wt = (temp * temp) * angular_speed;
            }
        }
    }
}
void high_func_CommandChange() {}
void high_func_L2() {}
void high_func_R2() {}
void high_func_TRI() 
{
}
void high_func_CIR() {}
void high_func_CRO() {}
void high_func_SQU() {}
void high_func_UP() 
{   }
void high_func_RIGHT() {}
void high_func_DOWN() {}
void high_func_LEFT() {}
void high_func_L1()
{
    if (!autoMode)
    {
        targetPoint = 0;
        maxPointCount = 1;
                
        tolerance.x = 0.01;
        tolerance.y = 0.01;
        tolerance.w = 0.1;

        targetPos.x = 4.1;              //+    startup_offset_x_encoder;
        targetPos.y = -3;              //+    startup_offset_y_encoder;
        targetPos.w = -165 * DEG_TO_RAD; //-    startup_offset_w_encoder;

        command = noAction;

        maxSpeed.x = 1.5;
        maxSpeed.y = 1.5;
        maxSpeed.w = 1.5;
        
        autoMode = true;
        motorUpdateTicker.attach(&motorUpdate, UPDATE_RATE);
    }
}
void high_func_L3() {}
void high_func_R1()
{
    if (autoMode)
    {
        targetPoint = 0;
        maxPointCount = 1;
                
        tolerance.x = 0.01;
        tolerance.y = 0.01;
        tolerance.w = 0.1;

        targetPos.x = 4.1;              //+    startup_offset_x_encoder;
        targetPos.y = -3;              //+    startup_offset_y_encoder;
        targetPos.w = -165 * DEG_TO_RAD; //-    startup_offset_w_encoder;

        command = noAction;

        maxSpeed.x = 1.5;
        maxSpeed.y = 1.5;
        maxSpeed.w = 1.5;
        
        autoMode = false;
        motorUpdateTicker.detach();
        motor.manual(); //This changes the acceleration to 99999;
        inverse(0,0,0);
    }
}
void high_func_R3() {}
void high_func_SHARE() 
{
    
}
void high_func_OPTIONS() {}
void low_func_CommandChange() {}
void low_func_LH()
{
    if (!autoMode)
    {
        vt = 0;
        vnt = 0;
    }
}
void low_func_RH()
{
    if (!autoMode)
    {
        wt = 0;
    }
}
void low_func_L2() {}
void low_func_R2() {}
void low_func_TRI() {}
void low_func_CIR() {}
void low_func_CRO() {}
void low_func_SQU() {}
void low_func_UP() {}
void low_func_RIGHT() {}
void low_func_DOWN() {}
void low_func_LEFT() {}
void low_func_L1() {}
void low_func_L3() {}
void low_func_R1() {}
void low_func_R3() {}
void low_func_SHARE() {}
void low_func_OPTIONS() {}
void fall_func_CommandChange() {}
void fall_func_LH()
{
    if (!autoMode)
    {
        vt = 0;
        vnt = 0;
    }
}
void fall_func_RH()
{
    if (!autoMode)
    {
        wt = 0;
    }
}
void fall_func_L2() {}
void fall_func_R2() {}
void fall_func_TRI() {}
void fall_func_CIR() {}
void fall_func_CRO() {}
void fall_func_SQU() {}
void fall_func_UP() {}
void fall_func_RIGHT() {}
void fall_func_DOWN() {}
void fall_func_LEFT() {}
void fall_func_R1()
{
    if (autoMode)
    {
        targetPoint = 0;
        maxPointCount = 1;
                
        tolerance.x = 0.01;
        tolerance.y = 0.01;
        tolerance.w = 0.1;

        targetPos.x = 4.1;              //+    startup_offset_x_encoder;
        targetPos.y = -3;              //+    startup_offset_y_encoder;
        targetPos.w = -165 * DEG_TO_RAD; //-    startup_offset_w_encoder;
        
        command = noAction;

        maxSpeed.x = 1.5;
        maxSpeed.y = 1.5;
        maxSpeed.w = 1.5;
        
        autoMode = false;
        motorUpdateTicker.detach();
    }
}
void fall_func_L3() {}
void fall_func_L1()
{
    if (!autoMode)
    {
        targetPoint = 0;
        maxPointCount = 1;
                
        tolerance.x = 0.01;
        tolerance.y = 0.01;
        tolerance.w = 0.1;

        targetPos.x = 4.1;              //+    startup_offset_x_encoder;
        targetPos.y = -3;              //+    startup_offset_y_encoder;
        targetPos.w = -165 * DEG_TO_RAD; //-    startup_offset_w_encoder;

        command = noAction;

        maxSpeed.x = 1.5;
        maxSpeed.y = 1.5;
        maxSpeed.w = 1.5;
        
        autoMode = true;
        motorUpdateTicker.attach(&motorUpdate, UPDATE_RATE);
    }
}
void fall_func_R3() {}
void fall_func_SHARE() {}
void fall_func_OPTIONS() {}
void rise_func_CommandChange() {}
void rise_func_LH() {}
void rise_func_RH() {}
void rise_func_L2() {}
void rise_func_R2() {}
void rise_func_TRI() 
{
    // if the button blocked for 500 ms or the button press for first time
    if(buttonBlock.read_ms() >= blockTime || firstPress)
    {
        firstPress = false;
        // Stop the timer
        buttonBlock.stop();
        // Send messege to slave
        slave.vesc();
        //slave.homing(); //<- For 3 pt
        //Debug
        //ps4PC.printf("VESC");
        //ps4PC.printf("the timer now is :%d \n",buttonBlock.read_ms());
        // Restart the timer
        buttonBlock.reset();
        buttonBlock.start();
        pc.printf("RISE TRI \n");
    }    
}
void rise_func_CIR() 
{
    // if the button blocked for 500 ms or the button press for first time
    if(buttonBlock.read_ms() >= blockTime || firstPress)
    {
        
        firstPress = false;
        // Stop the timer
        buttonBlock.stop();
        // Send messege to slave
        slave.fire();
        //Debug
        //ps4PC.printf("the timer now is :%d \n",buttonBlock.read_ms());
        //ps4PC.printf("Fire");       
        // Restart the timer
        buttonBlock.reset();
        buttonBlock.start();
    } 
}
void rise_func_CRO()
{
    // if the button blocked for 500 ms or the button press for first time
    if(buttonBlock.read_ms() >= blockTime || firstPress)
    {
        firstPress = false;
        // Stop the timer
        buttonBlock.stop();
        // Send messege to slave
        slave.charge();
        //Debug
        //ps4PC.printf("Stop");
        //ps4PC.printf("the timer now is :%d \n",buttonBlock.read_ms());
        // Restart the timer
        buttonBlock.reset();
        buttonBlock.start();
    }
    }
void rise_func_SQU() 
{
    // if the button blocked for 500 ms or the button press for first time
    if(buttonBlock.read_ms() >= blockTime || firstPress)
    {
        firstPress = false;
        // Stop the timer
        buttonBlock.stop();
        // Send messege to slave
        slave.homing();
        //slave.readyPosition(); //<- For 3 pt
        //Debug
        //ps4PC.printf("Homing");
        //ps4PC.printf("the timer now is :%d \n",buttonBlock.read_ms());
        // Restart the timer
        buttonBlock.reset();
        buttonBlock.start();
    }    
}
void rise_func_UP() 
{
    // if the button blocked for 500 ms or the button press for first time
    if(buttonBlock.read_ms() >= blockTime || firstPress)
    {
        firstPress = false;
        // Stop the timer
        buttonBlock.stop();
        // Send messege to slave
        slave.toggleVG();
        //Debug
        //ps4PC.printf("ToggleVG");
        // Restart the timer
        buttonBlock.reset();
        buttonBlock.start();
        pc.printf("RISE UP");
}    
    }
void rise_func_RIGHT() 
{
    // if the button blocked for 500 ms or the button press for first time
    if(buttonBlock.read_ms() >= blockTime || firstPress)
    {
        firstPress = false;
        // Stop the timer
        buttonBlock.stop();
        // Send messege to slave
        //slave.toggleHG();
        //slave.vesc();
        //Debug
        //ps4PC.printf("ToggleHG");
        // Restart the timer
        buttonBlock.reset();
        buttonBlock.start();
        pc.printf("RISE RIGHT");
    }       
}
void rise_func_DOWN() 
{
    // if the button blocked for 500 ms or the button press for first time
    if(buttonBlock.read_ms() >= blockTime || firstPress)
    {
        firstPress = false;
        // Stop the timer
        buttonBlock.stop();
        // Send messege to slave
        slave.toggleVS();
        //Debug
        //ps4PC.printf("ToggleVS");
        // Restart the timer
        buttonBlock.reset();
        buttonBlock.start();
        pc.printf("RISE DOWN");
}    
    }
void rise_func_LEFT() 
{
            // if the button blocked for 500 ms or the button press for first time
    if(buttonBlock.read_ms() >= blockTime || firstPress)
    {
        firstPress = false;
        // Stop the timer
        buttonBlock.stop();
        // Send messege to slave
        slave.toggleHS();
        //Debug
        //ps4PC.printf("toggleHS");
        // Restart the timer
        buttonBlock.reset();
        buttonBlock.start();
        pc.printf("RISE LEFT");
    } 
}
void rise_func_L1() {}
void rise_func_L3()
{
    if (!autoMode)
    {
        vt = 0;
        vnt = 0;
    }
}
void rise_func_R1() {}
void rise_func_R3()
{
    if (!autoMode)
    {
        wt = 0;
    }
}
void rise_func_SHARE() {}
void rise_func_OPTIONS() {}

~~~
