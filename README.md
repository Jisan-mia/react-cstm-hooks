# React Custom Hooks

1. useCountdown
```tsx
import { useEffect, useState } from 'react';

const useCountdown = (targetDate) => {
    const countDownDate = new Date(targetDate).getTime();



    const [countDown, setCountDown] = useState(
        countDownDate - new Date().getTime()
    );

    // console.log("from useCountrdown", countDown);

    useEffect(() => {
        const interval = setInterval(() => {
            setCountDown(countDownDate - new Date().getTime());
        }, 1000);

        return () => clearInterval(interval);
    }, [countDownDate]);

    // console.log("from useCountdown", getReturnValues(countDown));

    return getReturnValues(countDown);
};

const getReturnValues = (countDown) => {
    // calculate time left
    const days = Math.floor(countDown / (1000 * 60 * 60 * 24));
    const hours = Math.floor(
        (countDown % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)
    );
    const minutes = Math.floor((countDown % (1000 * 60 * 60)) / (1000 * 60));
    const seconds = Math.floor((countDown % (1000 * 60)) / 1000);

    // console.log("from getReturnValues", days, hours, minutes, seconds);

    return [days, hours, minutes, seconds];
};

export { useCountdown };
```