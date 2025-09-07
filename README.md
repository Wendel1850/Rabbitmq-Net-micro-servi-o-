using RabbitMQ.Client;
using System.Text;

namespace EstoqueApi.Services
{
    public class RabbitMqService
    {
        private readonly IConnection _connection;
        private readonly IModel _channel;

        public RabbitMqService(string rabbitMqConnectionString)
        {
            _connection = ConnectionFactory.CreateConnection(rabbitMqConnectionString);
            _channel = _connection.CreateModel();
        }

        public void SendMessage(string message)
        {
            var body = Encoding.UTF8.GetBytes(message);
            _channel.BasicPublish(exchange: "", routingKey: "estoque", body: body);
        }
    }
}
