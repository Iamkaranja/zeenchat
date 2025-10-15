# Voice Notes Feature Documentation

## Overview
ZeenChat now supports voice notes, allowing users to send audio messages in their conversations. This feature uses the Web MediaRecorder API for recording and stores audio files securely on the server.

## How to Use Voice Notes

### Recording a Voice Note

1. **Start Recording**
   - Click the microphone button (🎤) next to the message input field
   - Your browser will prompt for microphone permissions (first time only)
   - Grant permission to enable voice recording

2. **During Recording**
   - A red pulsing indicator shows recording is active
   - Live timer displays the current recording duration
   - Two options available:
     - **Cancel**: Discard the recording and return to chat
     - **Stop**: Finish recording and proceed to preview

3. **Preview Your Recording**
   - After stopping, you'll see a preview interface
   - Click the play button to listen to your recording
   - Options available:
     - **Re-record**: Discard current recording and start over
     - **Send**: Upload and send the voice note to the chat

4. **Sending**
   - Click Send to upload the voice note
   - A loading indicator shows upload progress
   - The voice note appears in the chat once sent

### Playing Received Voice Notes

- Voice notes appear as special message bubbles with:
  - A play button icon
  - Audio player controls
  - Duration display
  - Timestamp

- Click the play button or use the audio controls to listen
- Standard audio controls: play, pause, seek, volume

## Technical Details

### Supported Browsers
- Chrome/Edge (v49+)
- Firefox (v25+)
- Safari (v14.1+)
- Opera (v36+)

Note: Browser must support the MediaRecorder API

### Audio Format
- Format: WebM with Opus codec
- Quality: Default browser quality
- File size: Varies based on duration (typically ~10KB per second)

### Limitations
- Maximum recording duration: Limited by browser/device
- File size limits: Controlled by server configuration
- Browser permissions required for microphone access

## Privacy & Security

- Voice notes require user authentication
- Files stored securely in media directory
- CSRF protection on uploads
- Only chat participants can access voice notes
- Microphone access requires explicit user permission

## Troubleshooting

### Microphone Button Not Working
- Check browser permissions for microphone access
- Ensure you're using HTTPS (required for MediaRecorder API)
- Try refreshing the page

### Upload Failed
- Check your internet connection
- Ensure file isn't corrupted
- Try recording again

### Can't Play Voice Notes
- Ensure browser supports WebM/Opus audio
- Check audio output device
- Try refreshing the page

### No Sound During Recording
- Check system microphone is not muted
- Test microphone in other applications
- Check browser microphone permissions

## Development Notes

### File Structure
- Audio files stored in: `media/voice_notes/`
- Model: `Message.message_type = 'voice'`
- Upload endpoint: `/upload-voice-note/`

### WebSocket Events
- Type: `voice_message`
- Payload includes: sender, receiver, message_id, voice_url, duration, timestamp

### Database Fields
- `message_type`: CharField ('text' or 'voice')
- `voice_note`: FileField (audio file)
- `duration`: IntegerField (seconds)

## Future Enhancements

Potential improvements for future versions:
- Waveform visualization during recording
- Audio editing (trim, cut)
- Multiple audio format support
- Voice message forwarding
- Playback speed control
- Transcription services integration
- Offline recording support
