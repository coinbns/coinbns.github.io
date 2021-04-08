<?php

namespace App\Events;

use Illuminate\Broadcasting\Channel;
use Illuminate\Queue\SerializesModels;
use Illuminate\Broadcasting\PrivateChannel;
use Illuminate\Broadcasting\PresenceChannel;
use Illuminate\Foundation\Events\Dispatchable;
use Illuminate\Broadcasting\InteractsWithSockets;
use Illuminate\Contracts\Broadcasting\ShouldBroadcast;

class RecipientReadMessage implements ShouldBroadcast
{
    use InteractsWithSockets, SerializesModels;

    public $tradeId;
    public $recipientId;
    public $recipientReadAt;

    public function __construct($recipientId, $tradeId, $recipientReadAt)
    {
        $this->tradeId = $tradeId;
        $this->recipientId = $recipientId;
        $this->recipientReadAt = $recipientReadAt;
    }

    public function broadcastOn()
    {
        return new PresenceChannel('chat-trade.'.$this->tradeId);
    }
}

