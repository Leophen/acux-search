---
title: useUserMedia
---

用于获取用户媒体（视频和音频）的 hooks。

## 引入

```js
import {useUserMedia} from '@baidu/acud-pro-components';
```

## 基本用法

```jsx live
function App() {
    const videoRef = useRef();

    // 自定义 getUserMedia 参数
    const constraints = useMemo(() => ({
        video: true,
        audio: {
            sampleRate: 16000,
            sampleSize: 16,
            channelCount: 1
        }
    }), []);

    const handleSuccess = useCallback(stream => {
        const video = videoRef.current;
        video.srcObject = stream;
    }, []);

    const handleError = useCallback(error => {
        console.error('navigator.getUserMedia error: ', error);
    }, []);

    const {start, stop} = useUserMedia(constraints, handleSuccess, handleError);

    useEffect(() => {
        // 开启录制
        start();
        return () => {
            // 停止录制
            stop();
        };
    }, []);

    return (
        <div>
            <video
                ref={videoRef}
                autoPlay
                width="600"
                height="400"
            />
        </div>
    );
}
```

## API

```typescript static
export interface UserMediaResult {
    stream: MediaStream | null;
    recording: boolean;
    start: () => void;
    stop: () => void;
}

export function useUserMedia(
    constraints?: MediaStreamConstraints,
    onSuccess?: (stream: MediaStream) => void,
    onError?: (error: Error) => void
): UserMediaResult;
```
