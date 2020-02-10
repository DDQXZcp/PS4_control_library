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
