### STM32F407G-Disc1 (C)

#### GPIO-Pins

Um Interrupts zu verwenden muss man die jeweilige EXTI_Line Konfigurieren. Es gibt viele verschiedenen EXTI_Lines, welche für jeweils unterschiedliche PINS verantwortlich sind.[2,3,4]

|      Irq       |       Handler        |                 Description                 |
| :------------: | :------------------: | :-----------------------------------------: |
|   EXTI0_IRQn   |   EXTI0_IRQHandler   |    Handler for pins connected to line 0     |
|   EXTI1_IRQn   |   EXTI1_IRQHandler   |    Handler for pins connected to line 1     |
|   EXTI2_IRQn   |   EXTI2_IRQHandler   |    Handler for pins connected to line 2     |
|   EXTI3_IRQn   |   EXTI3_IRQHandler   |    Handler for pins connected to line 3     |
|   EXTI4_IRQn   |   EXTI4_IRQHandler   |    Handler for pins connected to line 4     |
|  EXTI9_5_IRQn  |  EXTI9_5_IRQHandler  |  Handler for pins connected to line 5 to 9  |
| EXTI15_10_IRQn | EXTI15_10_IRQHandler | Handler for pins connected to line 10 to 15 |

Danach muss man in der Callback-Funktion checken ob der gewünschte PIN gedrückt wurde.[3,4] 

```c
static void EXTILine0_Config(void) /* Für die 0-Pins*/
{
    GPIO_InitTypeDef   GPIO_InitStructure;

    /* Enable GPIOA clock */
    __HAL_RCC_GPIOA_CLK_ENABLE();

    /* Configure PA0 pin as input floating */
    GPIO_InitStructure.Mode = GPIO_MODE_IT_FALLING;
    GPIO_InitStructure.Pull = GPIO_NOPULL;
    GPIO_InitStructure.Pin = GPIO_PIN_0;
    HAL_GPIO_Init(GPIOA, &GPIO_InitStructure);

    /* Enable and set EXTI Line0 Interrupt to the lowest priority */
    HAL_NVIC_SetPriority(EXTI0_IRQn, 2, 0);
    HAL_NVIC_EnableIRQ(EXTI0_IRQn);
}
```

Die Callback Funktion

```c
void HAL_GPIO_EXTI_Callback(uint16_t GPIO_Pin)
{
    if(GPIO_Pin == KEY_BUTTON_PIN)
    {
        /* Do something */
    }
}
```

##### Konfiguration Optionen[2,3]

###### Mode

| Optionen                                    |
| ------------------------------------------- |
| GPIO_InitStruct.Mode = GPIO_MODE_IT_FALLING |
| GPIO_InitStruct.Mode = GPIO_MODE_AF_PP;     |
| GPIO_InitStruct.Mode = GPIO_MODE_INPUT;     |
| GPIO_InitStruct.Mode = GPIO_MODE_IT_RISING; |
| GPIO_InitStruct.Mode = GPIO_MODE_OUTPUT_PP; |

###### Pull

| Optionen                            |
| ----------------------------------- |
| GPIO_InitStruct.Pull = GPIO_NOPULL; |
| GPIO_InitStruct.Pull = GPIO_UP;     |
| GPIO_InitStruct.Pull = GPIO_DOWN;   |

###### Speed

| Optionen                                      |
| --------------------------------------------- |
| GPIO_InitStruct.Speed = GPIO_SPEED_FREQ_HIGH; |
| GPIO_InitStruct.Speed = GPIO_SPEED_FREQ_LOW;  |
| GPIO_InitStructure.Speed = GPIO_SPEED_FAST;   |
| GPIO_InitStructure.Speed = GPIO_SPEED_SLOW;   |

#### PINs auf High und Low setzen

```c
# High
HAL_GPIO_WritePin(GPIO_Gruppe, GPIO_PIN_Nummer, GPIO_PIN_SET);
# Low
HAL_GPIO_WritePin(GPIO_Gruppe, GPIO_PIN_Nummer, GPIO_PIN_RESET);
```

## Quellen

[1] : "Configuring GPIO on the STM32F4xx" [online](http://www.eas.uccs.edu/~mwickert/ece5655/lecture_notes/ARM/ece5655_appendixE.pdf) | zuletzt besucht 23.12.2019

[2] : "STM32F407G Reference Manuel - GPIO" [online]( https://www.st.com/content/ccc/resource/technical/document/user_manual/70/fe/4a/3f/e7/e1/4f/7d/DM00039084.pdf/files/DM00039084.pdf/jcr:content/translations/en.DM00039084.pdf) | zuletzt besucht 30.11.2019

[3] : "STM32F4 GPIO tutorial with unboard leds and button" [online](https://stm32f4-discovery.net/2014/04/stm32f429-discovery-gpio-tutorial-with-onboard-leds-and-button/) | zuletzt besucht 08.12.2019

[4] : "GPIO Pins on a STM32F4 Board" [online](https://microcontrollerslab.com/gpio-pins-of-smt32f4-discovery-board/) | zuletzt besucht 16.12.2019

