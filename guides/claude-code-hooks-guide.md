# Claude Code Hooks - Hướng Dẫn Ngắn Gọn

## Tổng Quan
Hooks là scripts tự động chạy tại các thời điểm nhất định trong Claude Code workflow.

## Cấu Trúc Cơ Bản
```
project/
├── .claude/
│   └── hooks/
│       └── pre-prompt.js    # Hook chạy trước khi xử lý prompt
└── prompts.txt             # File output (được tạo tự động)
```

## Tạo Hook Để Log Prompts

### Bước 1: Tạo thư mục
```bash
mkdir -p .claude/hooks
```

### Bước 2: Tạo file pre-prompt.js

```javascript
#!/usr/bin/env node
const fs = require('fs');

let prompt = '';
process.stdin.setEncoding('utf8');
process.stdin.on('readable', () => {
    const chunk = process.stdin.read();
    if (chunk !== null) prompt += chunk;
});

process.stdin.on('end', () => {
    try {
        fs.appendFileSync('prompts.txt', prompt + '\n');
        console.error('✅ Prompt logged');
    } catch (error) {
        console.error('❌ Log failed:', error.message);
    }
    process.stdout.write(prompt);  // QUAN TRỌNG: luôn trả về prompt
});
```

### Bước 3: Cấp quyền thực thi
```bash
chmod +x .claude/hooks/pre-prompt.js
```

### Bước 4: Test
```bash
echo "test prompt" | ./.claude/hooks/pre-prompt.js
```

## Kết Quả Thực Tế

Với hook trên, file `prompts.txt` sẽ chứa:
```
Rồi, kiểm tra lại xem
Giờ mới thấy nè
Viết lại cái hướng dẫn chi tiết đi, lấy cái vụ prompt này làm ví dụ, viết ngắn gọn, chính xác, step by step
```

## Các Loại Hook Khác

### post-prompt.js - Log responses
```javascript
#!/usr/bin/env node
const fs = require('fs');
const input = require('fs').readFileSync(0, 'utf8');

try {
    fs.appendFileSync('responses.txt', input + '\n---\n');
    console.error('✅ Response logged');
} catch (error) {
    console.error('❌ Log failed:', error.message);
}
process.stdout.write(input);
```

### gemini-prompt.js - Gọi Gemini CLI
```javascript
#!/usr/bin/env node
const fs = require('fs');
const { spawn } = require('child_process');

let prompt = '';
process.stdin.setEncoding('utf8');

process.stdin.on('readable', () => {
    const chunk = process.stdin.read();
    if (chunk !== null) prompt += chunk;
});

process.stdin.on('end', () => {
    // Pass through the original prompt first
    process.stdout.write(prompt);
    
    // Call Gemini CLI in the background
    const gemini = spawn('gemini', ['-p', prompt], {
        stdio: ['ignore', 'pipe', 'pipe'],
        detached: true
    });
    
    let geminiResponse = '';
    
    gemini.stdout.on('data', (data) => {
        geminiResponse += data.toString();
    });
    
    gemini.stderr.on('data', (data) => {
        console.error('Gemini CLI error:', data.toString());
    });
    
    gemini.on('close', () => {
        try {
            const timestamp = new Date().toLocaleString('vi-VN');
            const logEntry = `\n=== Gemini Response [${timestamp}] ===\nPrompt: ${prompt.trim()}\nResponse: ${geminiResponse.trim()}\n${'='.repeat(50)}\n`;
            
            fs.appendFileSync('gemini-responses.txt', logEntry);
            console.error('✅ Gemini response logged');
        } catch (error) {
            console.error('❌ Failed to log Gemini response:', error.message);
        }
    });
    
    // Don't wait for gemini to finish - let it run in background
    gemini.unref();
});
```

**Cấu hình trong .gemini/.env:**
```bash
GEMINI_API_KEY=your_api_key_here
GEMINI_MODEL=gemini-2.0-flash-exp  # Tùy chọn, mặc định là gemini-2.0-flash-exp
```

**Các model khả dụng:**
- `gemini-2.0-flash-exp` (mặc định)
- `gemini-1.5-flash`
- `gemini-1.5-pro`

### pre-prompt-timestamp.js - Thêm timestamp
```javascript
#!/usr/bin/env node
const input = require('fs').readFileSync(0, 'utf8');
const timestamp = new Date().toLocaleString('vi-VN');
const timestampedPrompt = `[${timestamp}] ${input}`;
process.stdout.write(timestampedPrompt);
```

## Quy Tắc Quan Trọng

1. **Luôn đọc từ stdin**: `process.stdin` hoặc `readFileSync(0)`
2. **Luôn ghi ra stdout**: `process.stdout.write()` 
3. **Log errors ra stderr**: `console.error()`
4. **Xử lý lỗi**: Trả về input gốc nếu thất bại

## Troubleshooting

**Hook không chạy?**
```bash
ls -la .claude/hooks/  # Kiểm tra quyền
```

**Test trực tiếp:**
```bash
echo "test" | ./.claude/hooks/pre-prompt.js
```